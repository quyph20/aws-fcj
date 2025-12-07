---
title: "Blog 1"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Triển khai quy trình phê duyệt đa bên cho các kho lưu trữ AWS Backup được cách ly về mặt logic

Các doanh nghiệp ngày nay đối mặt với những thách thức đáng kể trong việc bảo mật dữ liệu dự phòng trong các sự cố. Khi hệ thống sao lưu dùng chung xác thực với môi trường sản xuất, thông tin đăng nhập bị xâm phạm có thể chặn quyền truy cập vào cả hai môi trường, khiến doanh nghiệp dễ bị tổn thương trong quá trình khôi phục. Các doanh nghiệp có môi trường liên kết đối mặt với rủi ro cao hơn, trong đó các khung phê duyệt đơn lẻ không cung cấp sự bảo vệ đầy đủ.

Việc tích hợp khả năng Phê duyệt đa bên (Multi-party approval) với AWS Backup cung cấp một giải pháp mạnh mẽ cho thách thức này bằng cách tạo ra một đường dẫn truy cập độc lập, bảo mật cho các bản sao lưu, đảm bảo rằng dữ liệu dự phòng vẫn có thể truy cập được ngay cả khi các phương pháp xác thực truyền thống thất bại và tài khoản sở hữu kho dự phòng hoặc AWS Organizations bị xâm phạm. Phê duyệt đa bên đòi hỏi nhiều người phê duyệt để ủy quyền các hoạt động quan trọng, ngăn chặn các thay đổi đơn phương thông qua một quy trình ra quyết định phân tán và đảm bảo đường dẫn truy cập này vẫn an toàn.

Trong bài đăng trước của chúng tôi, chúng tôi đã đề cập đến các mối đe dọa mạng đối với cơ sở hạ tầng sao lưu, giới thiệu tính năng Phê duyệt đa bên [tích hợp với các kho được cách ly logic (logically air-gapped vaults)] mới, và giải thích các trụ cột của bảo vệ dữ liệu. Trong bài đăng này, chúng tôi sẽ cung cấp hướng dẫn triển khai chi tiết để cấu hình quy trình phê duyệt đa bên, bao gồm các phương pháp hay nhất và các ví dụ thực tế. Những hướng dẫn này sẽ giúp bạn thiết lập các cơ chế khôi phục an toàn, linh hoạt, duy trì quyền truy cập vào dữ liệu dự phòng quan trọng trong mọi trường hợp – từ các sự cố tài khoản đơn lẻ đến các sự kiện toàn doanh nghiệp.

---

## Các mô hình khôi phục

Trong Phần 1, chúng tôi đã giới thiệu hai mô hình khôi phục quan trọng được thiết kế để giải quyết các quy mô sự cố bảo mật khác nhau.

Mô hình khôi phục tài khoản AWS giải quyết các tình huống trong đó tài khoản lưu trữ kho được cách ly logic trở nên không thể truy cập được. Nó sử dụng các nhóm Phê duyệt đa bên để tạo ra một đường dẫn truy cập độc lập cần nhiều người phê duyệt. Điều này cho phép khôi phục ngay cả khi tài khoản sở hữu kho bị xâm phạm và xác thực truyền thống thất bại.

Mô hình khôi phục AWS Organizations giải quyết các tình huống trong đó toàn bộ cấu trúc Organizations bị xâm phạm. Nó thiết lập Organizations khôi phục riêng biệt với một nhà cung cấp danh tính (Identity provider) độc lập, duy trì quyền truy cập vào dữ liệu dự phòng trong các sự cố toàn Tổ chức.

Trong bài đăng này, chúng tôi sẽ chỉ cho bạn cách triển khai các bước cho cả hai mô hình và bao gồm các phương pháp hay nhất.


  
## Khôi phục tài khoản

 Các bước triển khai trong bài đăng này thiết lập quy trình Phê duyệt đa bên cho các tình huống khôi phục tài khoản như được tham chiếu trong sơ đồ kiến trúc sau.                                      |

---

Điều kiện tiên quyết (Prerequisites)
Việc triển khai này cần tối thiểu hai tài khoản AWS trong một Organization duy nhất.
Tài khoản Workload: Chứa môi trường sản xuất với kho dự phòng chính và các gói bảo vệ tài nguyên AWS. Sao chép các điểm khôi phục vào một kho được cách ly logic (tốt nhất là trong cùng một tài khoản hoặc một tài khoản sao lưu chuyên dụng).
Tài khoản Recovery: Cho phép tính liên tục của doanh nghiệp bằng cách yêu cầu quyền truy cập thông qua Phê duyệt đa bên để khôi phục dữ liệu quan trọng khi các hệ thống chính bị xâm phạm.
Trước khi bắt đầu triển khai, hãy hoàn thành các bước sau:
Bật AWS Backup và tạo một gói sao lưu.
Tạo một kho được cách ly logic.
Có một phiên bản AWS Identity Center đang hoạt động.
Ghi lại Tên tài nguyên Amazon (ARN) của kho được cách ly logic.
Cấu hình nhóm Phê duyệt đa bên của bạn
Trong phần này, chúng tôi mô tả các bước để thiết lập quy trình Phê duyệt đa bên đa tài khoản AWS.
1. Bật Phê duyệt đa bên trong tài khoản quản lý.
Khi bạn thiết lập Phê duyệt đa bên lần đầu, nó sẽ liên kết với Identity Center AWS Identity and Access Management (IAM) hiện có của bạn và tạo Cổng Phê duyệt (Approval Portal) để quản lý các yêu cầu, lời mời tham gia nhóm và xem các quyết định lịch sử (có sẵn trong tối đa 1 tháng).

a) Trong tài khoản quản lý Organizations, điều hướng đến Phê duyệt đa bên.

b) Thiết lập Phê duyệt đa bên để bật tính năng, sau đó chọn hoàn thành thiết lập (complete setup).

c) Trong bảng điều khiển AWS Backup, điều hướng đến Cài đặt > Quản lý đa tài khoản và bật Tích hợp Phê duyệt đa bên. Điều này được hiển thị trong hình sau.


Hình 2: Bật Tích hợp Phê duyệt đa bên
2. Tạo một nhóm Phê duyệt đa bên.

a) Điều hướng đến Organizations từ bảng điều khiển AWS của bạn và chọn Phê duyệt đa bên từ menu.

b) Tạo nhóm và cung cấp chi tiết của nhóm phê duyệt, với ngưỡng phê duyệt được đặt ở mức tối thiểu được khuyến nghị là hai người phê duyệt.

Phương pháp hay nhất: Ngưỡng tối thiểu của người phê duyệt đáng tin cậy (danh tính) là hai, điều này ngăn bất kỳ cá nhân nào truy cập dữ liệu dự phòng một cách đơn phương.

Hình 3: Biểu mẫu tạo Phê duyệt đa bên

3. Chấp nhận lời mời tham gia nhóm.

Mỗi người phê duyệt được chỉ định nhận được thông báo qua email để tham gia nhóm Phê duyệt đa bên. Ngoài ra, họ có thể truy cập cổng truy cập AWS để truy cập ứng dụng Cổng Phê duyệt (Approval Portal) để xem tất cả các yêu cầu.

a) Làm theo liên kết lời mời trong thông báo email. Ngoài ra, hãy truy cập cổng truy cập AWS để truy cập ứng dụng Cổng Phê duyệt để xem tất cả các yêu cầu.

b) Trong Cổng Phê duyệt, điều hướng đến tab Nhóm phê duyệt để tìm lời mời đang chờ xử lý và Chấp nhận.

Phương pháp hay nhất: Đảm bảo rằng những người phê duyệt hiểu trách nhiệm của họ và phản hồi kịp thời. Chia sẻ liên kết cổng thông qua các kênh ngoài băng tần (out-of-band channels) để truy cập nhanh hơn khi email bị trễ.

Hình 4: Lời mời tham gia nhóm phê duyệt đang chờ xử lý để người dùng ‘chấp nhận’ hoặc ‘từ chối’

Khi tất cả những người phê duyệt cần thiết đã chấp nhận, như được hiển thị trong hình trước, trạng thái nhóm sẽ thay đổi thành Hoạt động, như được hiển thị trong hình sau.

Hình 5: Nhóm phê duyệt hiện đang ở trạng thái Hoạt động

4. Chia sẻ nhóm phê duyệt với các tài khoản mục tiêu.

Các tài khoản mục tiêu bao gồm tất cả các tài khoản sở hữu kho được cách ly logic và các tài khoản khôi phục. Các tài khoản này cần nhóm Phê duyệt đa bên được chia sẻ với chúng để chúng có thể yêu cầu quyền truy cập vào các kho.

a) Điều hướng đến AWS Resource Access Manager (AWS RAM) trong tài khoản quản lý AWS nơi nhóm được tạo, như được hiển thị trong hình sau. Việc chia sẻ hiện phải được tạo trong Vùng AWS us-east-1.

Hình 6: Biểu mẫu AWS RAM để chia sẻ các nhóm phê duyệt

b) Chọn Tạo chia sẻ tài nguyên (Create resource share).

c) Cấu hình chi tiết nhóm với Nhóm Phê duyệt đa bên là loại tài nguyên, và chọn tài khoản khôi phục hoặc đơn vị tổ chức (OU) trong Chủ thể (Principals) trong Bước 3 của trình hướng dẫn.

d) Xem lại và Tạo chia sẻ tài nguyên.

Quan trọng: Việc chia sẻ này phải được chuẩn bị trước cho các tài khoản khôi phục quan trọng. Nếu không được thực hiện chủ động, bước này chỉ có thể được thực hiện trong một sự cố nếu tài khoản sở hữu nhóm vẫn có thể truy cập được.

5. Cấu hình Chính sách kiểm soát dịch vụ (SCPs) để quản lý việc sử dụng nhóm (tùy chọn).

Bạn có thể sử dụng SCP để hạn chế những nhóm phê duyệt nào có thể được liên kết với các kho được cách ly logic của bạn. Điều này tăng cường bảo mật bằng cách ngăn các nhóm trái phép truy cập các kho dự phòng quan trọng.
Ví dụ SCP:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "backup:AssociateMultiPartyApprovalTeam",
      "Resource": "*",
      "Condition": {
        "ArnNotLike": {
          "backup:MultiPartyApprovalTeamArn": "arn:aws:mpa:region:account-id:approval-team/team-id"
        }
      }
    }
  ]
}


6. Chấp nhận chia sẻ tài nguyên trong các tài khoản mục tiêu.

a) Trong mỗi tài khoản mục tiêu, điều hướng đến AWS Resource Access Manager.

b) Chọn Được chia sẻ với tôi > Chia sẻ tài nguyên.

c) Định vị lời mời đang chờ xử lý và Chấp nhận chia sẻ tài nguyên.

Hình 7: Lời mời người dùng chấp nhận hoặc từ chối chia sẻ tài nguyên từ tài khoản chính

7. Liên kết nhóm phê duyệt với kho được cách ly logic.

Theo các điều kiện tiên quyết, hãy đảm bảo rằng AWS Backup được bật trong tài khoản sở hữu kho và bạn đã tạo một kho được cách ly logic với các gói sao lưu thích hợp.

a) Điều hướng đến bảng điều khiển AWS Backup trong tài khoản sở hữu kho.

b) Chọn Kho dự phòng và chọn kho được cách ly logic hiện có của bạn.

c) Chỉ định nhóm phê duyệt bằng cách chọn nhóm phê duyệt được chia sẻ từ menu thả xuống, sau đó chọn Gửi, như được hiển thị trong hình sau.

Hình 8: Biểu mẫu chỉ định nhóm phê duyệt cho kho được cách ly logic...

8. Phê duyệt yêu cầu truy cập.

Các thành viên của nhóm Phê duyệt đa bên sẽ nhận được thông báo qua email về yêu cầu truy cập mới, hoặc họ có thể truy cập Cổng Phê duyệt (Approval Portal).

a) Trong Cổng Phê duyệt, điều hướng đến tab Yêu cầu (Requests) để xem yêu cầu.

b) Xem xét chi tiết yêu cầu, chọn đồng ý (Approve) và cung cấp lý do (tùy chọn nhưng được khuyến nghị).

c) Lặp lại bước này cho đến khi đạt được ngưỡng phê duyệt đã định.

Hình 9: Xem xét và phê duyệt yêu cầu truy cập kho dự phòng

Hình 10: Yêu cầu truy cập kho đã được phê duyệt
Khi đạt đủ ngưỡng phê duyệt, nhóm Phê duyệt đa bên sẽ cấp quyền truy cập vào kho được cách ly logic, tạo một kho dự phòng truy cập khôi phục trong tài khoản khôi phục.

Hình 11: Kho được cách ly logic hiện đã có sẵn cho các hoạt động khôi phục
Phương pháp hay nhất: Mặc dù các yêu cầu truy cập chỉ có thể đến từ các Tài khoản AWS có chia sẻ RAM đã thiết lập, những người phê duyệt vẫn nên xác minh tính hợp pháp và tính cấp bách của yêu cầu thông qua các kênh giao tiếp ngoài băng tần (out-of-band communication channels) trước khi phê duyệt.

10. Thực hiện các thao tác khôi phục.

a) Trong tài khoản khôi phục, điều hướng đến bảng điều khiển AWS Backup và chọn Kho dự phòng (Vaults).

b) Trong mục Các kho có thể truy cập thông qua Phê duyệt đa bên, kho mới có thể truy cập sẽ xuất hiện dưới Các kho dự phòng truy cập Khôi phục (Restore access backup vaults).

c) Duyệt các điểm khôi phục từ kho được cách ly logic nguồn.

d) Chọn một Điểm khôi phục (Recovery point), chọn thao tác Khôi phục (Restore), và hoàn tất việc khôi phục, như được hiển thị trong hình sau.
Phương pháp hay nhất: Cân nhắc sao chép các điểm khôi phục đã chọn sang các tài khoản/Vùng thay thế. Tài liệu hóa quy trình khôi phục và các thách thức để cải thiện các quy trình trong tương lai.

Hình 12: Các điểm khôi phục để khôi phục hoặc sao chép từ kho được cách ly logic
Các quy trình quản lý Phê duyệt đa bên khác

Ngoài các tình huống khôi phục, Phê duyệt đa bên còn hỗ trợ quản lý kho đang diễn ra thông qua hai quy trình quan trọng khác:

Thay đổi Chỉ định Nhóm (Changing Team Assignment): Từ tài khoản sở hữu kho (AWS Backup > Vaults), chọn kho, và Yêu cầu thay đổi nhóm phê duyệt (Request approval team change). Chọn nhóm mới và Gửi yêu cầu (Send request). Nhóm phê duyệt hiện tại phải phê duyệt yêu cầu này.

Thu hồi Quyền truy cập (Revoking Access): Trong tài khoản sở hữu kho (AWS Backup > Vaults), chọn kho, và điều hướng đến phần Truy cập thông qua phê duyệt đa bên (Access through multi-party approval). Tìm Kho dự phòng truy cập Khôi phục (Restore access backup vault), chọn Yêu cầu gỡ bỏ quyền truy cập kho (Request to remove vault access), và chọn Gửi yêu cầu. Nhóm phê duyệt hiện tại phải phê duyệt yêu cầu này.

Khôi phục Organization (Organization recovery)

Trong phần này, chúng tôi đề cập đến các bước triển khai cần thiết để thiết lập quy trình Phê duyệt đa bên cho các tình huống khôi phục đa Organization (cross-Organization) như được tham chiếu trong sơ đồ kiến trúc sau.

Hình 13: Quy trình phê duyệt đa bên đa Organization

Điều kiện tiên quyết (Prerequisites)

Việc triển khai này cần tối thiểu hai tài khoản AWS trong hai Organization khác nhau.

Trước khi đi sâu vào triển khai, hãy đảm bảo rằng bạn đã có những điều sau:

Đã bật AWS Backups và đã tạo một gói sao lưu

Đã tạo một kho được cách ly logic

Đã ghi lại ARN của kho được cách ly logic, vì điều này là cần thiết trong các bước khôi phục

Đã thiết lập một Organization khôi phục

Đã thiết lập một IdP (nhà cung cấp danh tính) độc lập

Phương pháp hay nhất: Sử dụng một nhà cung cấp IdP khác so với nhà cung cấp chính để tránh sự phụ thuộc chung. IdP này chỉ cần duy trì những người phê duyệt đa bên, không cần triển khai đầy đủ.

Cấu hình nhóm Phê duyệt đa bên của bạn

Trong phần này, chúng tôi mô tả các bước để thiết lập quy trình Phê duyệt đa bên đa Organization.

Trong Organization khôi phục của bạn, hoàn thành Các bước 1-3 từ phần Khôi phục tài khoản, thêm những người phê duyệt từ IdP bên ngoài của bạn khi tạo nhóm, sau đó tiếp tục đến Bước 4. Bạn cũng có thể áp dụng nguyên tắc đặc quyền tối thiểu bằng cách sử dụng SCP để hạn chế những nhóm nào có thể được liên kết với các kho được cách ly logic.

4. Chia sẻ nhóm phê duyệt với Organization chính.

a) Trong Organization khôi phục, điều hướng đến AWS RAM.

b) Chọn Tạo chia sẻ tài nguyên (Create resource share).

c) Cấu hình chia sẻ tài nguyên và chọn Nhóm Phê duyệt đa bên là loại tài nguyên, như được hiển thị trong hình sau.

Hình 14: Biểu mẫu chia sẻ tài nguyên của nhóm Phê duyệt đa bên

d) Trong Cấp quyền truy cập cho chủ thể (Grant access to principals), chọn Cho phép chia sẻ với bất kỳ ai (Allow sharing with anyone) và nhập ID tài khoản của tài khoản AWS lưu trữ kho được cách ly logic của bạn trong Organization chính.

e) Xem lại và Tạo chia sẻ tài nguyên.

Phương pháp hay nhất: Thử nghiệm chia sẻ đa Organization trong các bài tập khôi phục thường xuyên.

Hình 15: Chia sẻ tài nguyên để cấp quyền truy cập vào tài nguyên giữa các tổ chức

5. Chấp nhận chia sẻ tài nguyên trong Organization chính.

a) Trong tài khoản của Organization chính lưu trữ kho được cách ly logic, điều hướng đến AWS RAM.

b) Chọn Được chia sẻ với tôi > Chia sẻ tài nguyên.

c) Định vị lời mời đang chờ xử lý từ Organization khôi phục và Chấp nhận chia sẻ tài nguyên. Khi được chấp nhận, nhóm phê duyệt từ Organization khôi phục sẽ có sẵn để sử dụng, như được hiển thị trong hình sau.

Phương pháp hay nhất: Xác minh chi tiết chia sẻ tài nguyên cẩn thận trước khi chấp nhận để đảm bảo rằng đó là từ Organization khôi phục hợp pháp của bạn.

Hình 16: Yêu cầu phê duyệt chia sẻ nhóm Phê duyệt đa bên giữa các Organization

6. Liên kết nhóm phê duyệt với kho được cách ly logic.

a) Điều hướng đến bảng điều khiển AWS Backup trong tài khoản sở hữu kho.

b) Chọn kho được cách ly logic hiện có và chọn Chỉ định nhóm phê duyệt, như được hiển thị trong hình sau**.**

Hình 17: Biểu mẫu chỉ định nhóm phê duyệt cho kho được cách ly logic mà bạn muốn khôi phục

c) Chọn nhóm phê duyệt được chia sẻ từ Organization khôi phục và chọn Gửi.

Phương pháp hay nhất: Xác minh rằng liên kết thành công và kiểm tra quy trình phê duyệt trước khi sự cố thực tế xảy ra.

Quy trình khôi phục trong quá trình truy cập bị xâm phạm

Tiếp theo, chúng tôi đề cập đến các bước khôi phục cho trường hợp Organization chính của bạn chứa các kho dự phòng được cách ly logic trở nên không thể truy cập được do sự cố bảo mật hoặc thông tin đăng nhập bị xâm phạm.

7. Bắt đầu yêu cầu chia sẻ kho.

a) Từ một tài khoản khôi phục trong Organization khôi phục, điều hướng đến AWS Backup.

b) Chọn Kho dự phòng > Các kho có thể truy cập thông qua Phê duyệt đa bên.

c) Chọn Yêu cầu truy cập kho và nhập ARN của kho được cách ly logic vào biểu mẫu yêu cầu, như được hiển thị trong hình sau.


Hình 18: Biểu mẫu yêu cầu truy cập kho được cách ly logic mà bạn muốn khôi phục

d) Cung cấp Tên Kho Dự phòng Truy cập Khôi phục mô tả được tạo (tùy chọn nhưng được khuyến nghị để dễ nhận dạng hơn).

e) Gửi yêu cầu.

Hình 19: Các điểm khôi phục để khôi phục hoặc sao chép từ kho được cách ly logic
Kết luận

Việc sử dụng Phê duyệt đa bên với AWS Backup và triển khai nó trên các thiết lập đa tài khoản hoặc đa Organization cung cấp cho bạn một tư thế khôi phục có tính đàn hồi cao, nhiều lớp. Các bước được nêu trong hướng dẫn này cho phép bạn thiết lập cơ chế khôi phục linh hoạt hoạt động độc lập với cơ sở hạ tầng xác thực chính của bạn.

Việc triển khai này giải quyết thách thức cơ bản là duy trì quyền truy cập vào các bản sao lưu của bạn khi môi trường chính của bạn bị xâm phạm. Quy trình phê duyệt phân tán đảm bảo rằng không một cá nhân nào có thể truy cập dữ liệu dự phòng một cách đơn phương, trong khi cơ sở hạ tầng danh tính riêng biệt cho việc khôi phục Organization cung cấp mức độ đàn hồi cao nhất.

Chiến lược khôi phục của bạn phải được thực hiện thường xuyên để duy trì hiệu quả. Tích hợp các quy trình làm việc này vào thử nghiệm khôi phục thảm họa của bạn, tài liệu hóa các quy trình rõ ràng và đào tạo các nhóm của bạn về cả việc triển khai kỹ thuật và quy trình phê duyệt. Thường xuyên đánh giá các nhóm của bạn để các nhóm vẫn hoạt động với số lượng người phê duyệt tối thiểu có sẵn, đảm bảo rằng họ không bị ảnh hưởng bởi việc nhân viên nghỉ việc hoặc thay đổi vai trò.

Khi các mối đe dọa mạng tiếp tục phát triển, khả năng khôi phục nhanh chóng và hoàn toàn ngày càng trở nên quan trọng. Phê duyệt đa bên cho các kho được cách ly logic AWS Backup cung cấp các công cụ cần thiết để bảo vệ tài sản có giá trị nhất của doanh nghiệp bạn—dữ liệu của nó.
