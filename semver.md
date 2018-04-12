Phiên bản Ngữ nghĩa 2.0.0
==============================

Tóm lược
-------

Cho một số phiên bản MAJOR.MINOR.PATCH, tăng dần:

1. MAJOR khi bạn thực hiện các thay đổi API không tương thích,
1. MINOR khi bạn thêm chức năng tương thích ngược, và
1. PATCH khi bạn thực hiện các sửa lỗi các tương thích ngược .

Bổ sung nhãn cho trước khi phát hành và xây dựng metadata có sắn như các extension đến định dạng MAJOR.MINOR.PATCH.

Giới thiệu
------------

Trong thế giới của quản lý phần mềm tồn tại một nơi sợ hãi được gọi là
"địa ngục phụ thuộc". Hệ thống của bạn càng lớn và bạn càng có nhiều gói tích hợp vào phần mềm của bạn, bạn càng có nhiều khả năng tìm thấy chính mình, một ngày, trong cái hố tuyệt vọng này.

Trong các hệ thống có nhiều phụ thuộc, việc phát hành phiên bản gói mới có thể nhanh chóng trở thành cơn ác mộng. Nếu thông số kỹ thuật phụ thuộc quá chặt chẽ, bạn đang nguy hiểm ở trong phiên bản lock (không thể nâng cấp một gói mà không cần phải phát hành phiên bản mới của mỗi gói phụ thuộc). Nếu phụ thuộc được chỉ định quá lỏng lẻo, you will inevitably be bitten by version promiscuity
(giả định khả năng tương thích với các phiên bản trong tương lai hơn là hợp lý).
Địa ngục phụ thuộc là nơi bạn có mặt khi phiên bản khóa và / hoặc phiên bản quảng cáo ngăn không cho bạn di chuyển dự án một cách dễ dàng và an toàn.

Là một giải pháp cho vấn đề này, tôi đề xuất một bộ quy tắc đơn giản và yêu cầu mà chỉ ra cách số phiên bản được chỉ định và tăng lên.
Các quy tắc này dựa trên nhưng không nhất thiết giới hạn ở các các thông lệ phổ biến rộng rãi được sử dụng trong cả phần mềm đóng và mã nguồn mở.
Để hệ thống này hoạt động, trước hết bạn phải khai báo một API công khai. Điều này có thể bao gồm tài liệu hoặc được thực thi bởi chính nó. Bất kể, đó là quan trọng là API này phải rõ ràng và chính xác. Sau khi bạn xác định công khai API, bạn giao tiếp thay đổi nó với các gia số cụ thể cho số phiên bản của bạn. Xem xét một định dạng phiên bản của X.Y.Z (Major.Minor.Patch). Sửa lỗi không
ảnh hưởng đến sự gia tăng API phiên bản vá, tương thích ngược API
bổ sung / thay đổi tăng phiên bản phụ, và ngược không tương thích với API
thay đổi tăng phiên bản chính.

Tôi gọi hệ thống này là "Phiên bản Ngữ nghĩa" (Semantic Versioning). Theo chương trình này, số phiên bản
và cách họ thay đổi truyền đạt ý nghĩa về mã bên dưới và những gì đã
đã được sửa đổi từ phiên bản này sang phiên bản kế tiếp.

Đặc tả phiên bản ngữ nghĩa (SemVer)
------------------------------------------

Các từ khoá "PHẢI", "KHÔNG CẦN", "BĂT BUỘC", "SẼ", "SẼ KHÔNG", "NÊN", "NÊN KHÔNG", "KHUYẾN NGHỊ", "CÓ THỂ", và "OPTIONAL" trong tài liệu này sẽ được giải thích như mô tả trong [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Phần mềm sử dụng phiên bản ngữ nghĩa PHẢI khai báo một API công khai. API này
có thể được khai báo trong chính nó hoặc tồn tại trong tài liệu.
Tuy nhiên nó được thực hiện, nó nên được tốm lược và bao quát.

1. Một số phiên bản bình thường phải có dạng X.Y.Z nơi X, Y, và Z là
số nguyên không âm, và KHÔNG ĐƯỢC chứa số 0 trước. X là
phiên bản chính, Y là phiên bản nhỏ, và Z là phiên bản vá lỗi.
Mỗi phần tử PHẢI tăng theo số lượng. Ví dụ: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Một khi gói phiên bản đã được phát hành, nội dung của phiên bản đó KHÔNG ĐƯỢC sửa đổi. Bất kỳ sửa đổi nào PHẢI được phát hành dưới dạng một phiên bản mới.

1. Phiên bản chính zero (0.y.z) dành cho sự phát triển ban đầu. Mọi thứ có thể thay đổi bất cứ lúc nào. API công khai KHÔNG NÊN được coi là ổn định.

1. Phiên bản 1.0.0 định nghĩa API công khai. Cách thức mà số phiên bản được tăng lên sau khi bản phát hành này phụ thuộc vào API công khai này và cách nó 56 thay đổi.

1. Phiên bản vá Z (x.y.Z | x > 0) PHẢI được gia tăng nếu chỉ sửa lỗi tương thích được giới thiệu. Sửa lỗi được định nghĩa là thay đổi nội bộ để sửa chữa hành vi không chính xác.

1. Phiên bản Y (x.Y.z | x> 0) PHẢI được tăng lên nếu tương thích ngược mới được giới thiệu với public API. Nó phải là
tăng nếu bất kỳ chức năng public API nào được đánh dấu là không dùng nữa. Nó có thể
tăng nếu các tính năng hoặc cải tiến đáng kể mới được giới thiệu
trong mã cá nhân. Nó CÓ THỂ bao gồm các thay đổi mức vá. Phiên bản vá
PHẢI được đặt lại thành 0 khi phiên bản nhỏ được tăng lên.

1. Phiên bản chính X (X.y.z | X > 0) PHẢI được tăng nếu có những thay đổi không tương thích ngược lại được giới thiệu với public API. Nó cũng có thể bao gồm cả phiên bản phụ và thay đổi mức vá. Bản vá lỗi và phiên bản phụ PHẢI được đặt lại thành 0 khi phiên bản chính được tăng lên.

1. Một phiên bản tiền phát hành có thể được biểu thị bằng cách thêm dấu gạch nối và hàng loạt ký hiệu nhận dạng dấu chấm ngay sau dấu  phiên bản vá. Các số nhận dạng PHẢI chỉ bao gồm chữ, số và dấu gạch ngang của ASCII
[0-9A-Za-z-]. Các số nhận dạng PHẢI KHÔNG trống. Số nhận dạng số PHẢI KHÔNG bao gồm bắt đầu bằng 0. Các phiên bản tiền phát hành có ư utieen thấp hơn phiên bản bình thường kết hợp.
chỉ ra rằng phiên bản không ổn định và có thể không thỏa mãn yêu cầu về tính tương thích mong muốn như được biểu thị bởi các phiên bản bình thường. Ví dụ: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 71 1.0.0-x.7.z.92.

1. Xây dựng metadata CÓ THỂ được biểu thị bằng cách thêm dấu cộng và một dải dấu chấm các định danh được phân tách ngay lập tức sau bản vá hoặc phiên bản trước khi phát hành.
Các số nhận dạng PHẢI chỉ bao gồm chữ, số và dấu gạch ngang của ASCII [0-9A-Za-z-].
Số nhận dạng PHẢI KHÔNG rỗng. Xây dựng metadata PHẢI bị bỏ qua khi xác định phiên bản ưu tiên. Do đó hai phiên bản khác nhau chỉ trong xây dựng metadata, có cùng độ ưu tiên. Ví dụ: 1.0.0-alpha+001, 1.0.0+20130313144700,
1.0.0-beta+exp.sha.5114f85.

1. Sự ưu tiên đề cập đến cách các phiên bản được so sánh với nhau khi được yêu cầu.
Ưu tiên phải được tính bằng cách tách phiên bản thành các phần chính, nhỏ, vá
và định danh tiền phát hành theo thứ tự đó (Xây dựng siêu dữ liệu không hình
thành ưu tiên). Ưu tiên được xác định bởi sự khác biệt đầu tiên khi so sánh mỗi một trong số các số nhận dạng từ trái sang phải như sau: Các phiên bản chính, nhỏ và vá thường được so sánh về số lượng. Ví dụ: 1.0.0 < 2.0.0 <
2.1.0 < 2.1.1. Khi chính, phụ và vá đều như nhau, một phiên bản tiền phát hành được ưu tiên thấp hơn một phiên bản bình thường. Ví dụ: 1.0.0-alpha < 1.0.0. Ưu tiên cho hai phiên bản trước khi phát hành với cùng một phiên bản chính, nhỏ và vá lỗi PHẢI
được xác định bằng cách so sánh mỗi mã nhận dạng được phân tách từ trái sang phải
cho đến khi một sự khác biệt được tìm thấy như sau: định danh chỉ gồm các chữ số
được so sánh số và xác định với chữ cái hoặc dấu gạch nối được so sánh
liên quan theo thứ tự sắp xếp ASCII. Các định danh số luôn luôn có ưu tiên thấp hơn hơn số nhận dạng không phải là số. Một tập hợp lớn hơn các trường tiền phát hành có mức cao hơn ưu tiên hơn một tập hợp nhỏ hơn, nếu tất cả các định danh trước đều bằng nhau.
Ví dụ: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta <
1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

Mẫu ngữ pháp Backus-Naur cho các phiên bản SemVer hợp lệ
--------------------------------------------------

    <valid semver> ::= <version core>
                     | <version core> "-" <pre-release>
                     | <version core> "+" <build>
                     | <version core> "-" <pre-release> "+" <build>

    <version core> ::= <major> "." <minor> "." <patch>

    <major> ::= <numeric identifier>

    <minor> ::= <numeric identifier>

    <patch> ::= <numeric identifier>

    <pre-release> ::= <dot-separated pre-release identifiers>

    <dot-separated pre-release identifiers> ::= <pre-release identifier>
                                              | <pre-release identifier> "." <dot-separated pre-release identifiers>

    <build> ::= <dot-separated build identifiers>

    <dot-separated build identifiers> ::= <build identifier>
                                        | <build identifier> "." <dot-separated build identifiers>

    <pre-release identifier> ::= <alphanumeric identifier>
                               | <numeric identifier>

    <build identifier> ::= <alphanumeric identifier>
                         | <digits>

    <alphanumeric identifier> ::= <non-digit>
                                | <non-digit> <identifier characters>
                                | <identifier characters> <non-digit>
                                | <identifier characters> <non-digit> <identifier characters>

    <numeric identifier> ::= "0"
                           | <positive digit>
                           | <positive digit> <digits>

    <identifier characters> ::= <identifier character>
                              | <identifier character> <identifier characters>

    <identifier character> ::= <digit>
                             | <non-digit>

    <non-digit> ::= <letter>
                  | "-"

    <digits> ::= <digit>
               | <digit> <digits>

    <digit> ::= "0"
              | <positive digit>

    <positive digit> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

    <letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
               | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
               | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d"
               | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n"
               | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x"
               | "y" | "z"


Tại sao sử dụng phiên bản ngữ nghĩa?
----------------------------

Đây không phải là 1 ý kiến mới hay đột phá nào cả. Trên thực tế, bạn hẳn là làm điều gì gần giống như vậy rồi. Vấn đề là "gần giống" ở đây không đủ tốt. Nếu không tuân thủ theo 1 tập các đặc điểm kỉ thuật chính thức, các số phiên bản thực chất sẽ vô nghĩa cho việc quản lý sự phụ thuộc. Bằng cách đưa các định nghĩa rõ ràng cho các ý tưởng trên, nó trở nên dễ dàng trong việc liên kết các ý tưởng của bạn tới các người dùng phần mềm. Ngay khi những ý định được rõ ràng, Các đặc điểm kĩ thuật phụ thuốc linh động ( nhưng không quá linh động) cuối cùng cũng được hình thành.

Một ví dụ đơn giản sẽ cho thấy cách phiên bản ngữ nghĩa có thể làm cho sự phụ thuộc
địa ngục là một điều của quá khứ. Xem xét một thư viện có tên "Firetruck". Nó đòi hỏi một
Semantically Versioned gói có tên là "Ladder". Vào thời điểm Firetruck là
tạo ra, Ladder là ở phiên bản 3.1.0. Vì Firetruck sử dụng một số chức năng
lần đầu tiên được giới thiệu trong 3.1.0, bạn có thể chỉ định Ladder một cách an toàn
phụ thuộc lớn hơn hoặc bằng 3.1.0 nhưng nhỏ hơn 4.0.0. Bây giờ thì ở đâu
Phiên bản Ladder 3.1.1 và 3.2.0 trở nên có sẵn, bạn có thể thả chúng vào
hệ thống quản lý gói hàng và biết rằng chúng sẽ tương thích với
phần mềm phụ thuộc.

Là một nhà phát triển có trách nhiệm, bạn sẽ, tất nhiên, muốn xác minh rằng bất kỳ
gói nâng cấp chức năng như quảng cáo. Thế giới thực là một nơi lộn xộn;
không có gì chúng ta có thể làm được về điều đó nhưng phải thận trọng. Bạn có thể làm gì
Phiên bản ngữ nghĩa cung cấp cho bạn một cách hợp lí để phát hành và nâng cấp
gói mà không phải cuộn phiên bản mới của gói phụ thuộc, tiết kiệm cho bạn
thời gian và rắc rối.

Nếu tất cả điều này là mong muốn, tất cả những gì bạn cần làm để bắt đầu sử dụng phiên bản ngũ nghĩa là tuyên bố rằng bạn đang làm như vậy và sau đó làm theo các quy tắc. Liên kết
đến trang web này từ README của bạn để những người khác biết các quy tắc và có thể hưởng lợi từ nó.


Câu hỏi thường gặp
---

### How should I deal with revisions in the 0.y.z initial development phase?

The simplest thing to do is start your initial development release at 0.1.0
and then increment the minor version for each subsequent release.

### How do I know when to release 1.0.0?

If your software is being used in production, it should probably already be
1.0.0. If you have a stable API on which users have come to depend, you should
be 1.0.0. If you're worrying a lot about backwards compatibility, you should
probably already be 1.0.0.

### Doesn't this discourage rapid development and fast iteration?

Major version zero is all about rapid development. If you're changing the API
every day you should either still be in version 0.y.z or on a separate
development branch working on the next major version.

### If even the tiniest backwards incompatible changes to the public API require a major version bump, won't I end up at version 42.0.0 very rapidly?

This is a question of responsible development and foresight. Incompatible
changes should not be introduced lightly to software that has a lot of
dependent code. The cost that must be incurred to upgrade can be significant.
Having to bump major versions to release incompatible changes means you'll
think through the impact of your changes, and evaluate the cost/benefit ratio
involved.

### Documenting the entire public API is too much work!

It is your responsibility as a professional developer to properly document
software that is intended for use by others. Managing software complexity is a
hugely important part of keeping a project efficient, and that's hard to do if
nobody knows how to use your software, or what methods are safe to call. In
the long run, Semantic Versioning, and the insistence on a well defined public
API can keep everyone and everything running smoothly.

### What do I do if I accidentally release a backwards incompatible change as a minor version?

As soon as you realize that you've broken the Semantic Versioning spec, fix
the problem and release a new minor version that corrects the problem and
restores backwards compatibility. Even under this circumstance, it is
unacceptable to modify versioned releases. If it's appropriate,
document the offending version and inform your users of the problem so that
they are aware of the offending version.

### What should I do if I update my own dependencies without changing the public API?

That would be considered compatible since it does not affect the public API.
Software that explicitly depends on the same dependencies as your package
should have their own dependency specifications and the author will notice any
conflicts. Determining whether the change is a patch level or minor level
modification depends on whether you updated your dependencies in order to fix
a bug or introduce new functionality. I would usually expect additional code
for the latter instance, in which case it's obviously a minor level increment.

### What if I inadvertently alter the public API in a way that is not compliant with the version number change (i.e. the code incorrectly introduces a major breaking change in a patch release)?

Use your best judgment. If you have a huge audience that will be drastically
impacted by changing the behavior back to what the public API intended, then
it may be best to perform a major version release, even though the fix could
strictly be considered a patch release. Remember, Semantic Versioning is all
about conveying meaning by how the version number changes. If these changes
are important to your users, use the version number to inform them.

### How should I handle deprecating functionality?

Deprecating existing functionality is a normal part of software development and
is often required to make forward progress. When you deprecate part of your
public API, you should do two things: (1) update your documentation to let
users know about the change, (2) issue a new minor release with the deprecation
in place. Before you completely remove the functionality in a new major release
there should be at least one minor release that contains the deprecation so
that users can smoothly transition to the new API.

### Does SemVer have a size limit on the version string?

No, but use good judgment. A 255 character version string is probably overkill,
for example. Also, specific systems may impose their own limits on the size of
the string.

### Is "v1.2.3" a semantic version?

No, "v1.2.3" is not a semantic version. However, prefixing a semantic version
with a "v" is a common way (in English) to indicate it is a version number.
Abbreviating "version" as "v" is often seen with version control. Example:
`git tag v1.2.3 -m "Release version 1.2.3"`, in which case "v1.2.3" is a tag
name and the semantic version is "1.2.3".


About
-----

The Semantic Versioning specification is authored by [Tom
Preston-Werner](http://tom.preston-werner.com), inventor of Gravatar and
cofounder of GitHub.

If you'd like to leave feedback, please [open an issue on
GitHub](https://github.com/mojombo/semver/issues).


License
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
