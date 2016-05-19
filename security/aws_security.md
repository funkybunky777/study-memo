# AWS 보안 모범 사례

AWS Security Best Practices : [http://media.amazonwebservices.com/AWS_Security_Best_Practices.pdf](http://media.amazonwebservices.com/AWS_Security_Best_Practices.pdf)

## AWS 책임 분담 모델

AWS는 보안 인프라와 서비스를 제공하고 고객은 보안 운영 체제, 플랫폼, 데이터를 책임진다. 보안 글로벌 인프라를 위해 AWS는 인프라 구성 요소를 구성하고 사용자 및 사용자 권한을 AWS 서비스 하위 세트로 관리하는 IAM 서비스 등 보안 강화에 사용할 수 있는 서비스와 기능을 제공한다. 보안 서비스를 위해 AWSㄴㄴ 제공하는 다양한 유형의 서비스별 책임 분담 모델을 제공한다.

* 인프라 서비스
* 컨테이너 서비스
* 추상화된 서비스

EC2와 같은 인프라 서비스의 책임 분담 모델은 AWS가 다음 자산의 보안을 관리한다.

* 시설
* 하드웨어의 물리적 보안
* 네트워크 인프라
* 가상화 인프라

ISMS 자산 정의에 따라 AWS를 이러한 자산의 소유자로 간주하고 이러한 AWS 컨트롤을 활용하고 여러분의 ISMS에 포함시켜라.

EC2를 예로 든다면, 여러분은 다음 자산들에 대한 보안 책임이 있다.

* AMIs
* OS
* Applications
* Data in transit
* Data at rest
* Data stores
* Credentials
* Policies nd configuration


## Understanding the AWS secure global infrastructure

AWS가 관리하는 AWS 보안 글로벌 인프라와 서비스는 엔터프라이즈 시스템과 개별 애플리케이션을 위해 신뢰할
수 있는 기반을 제공합니다. AWS는 클라우드 내 정보 보안에 대한 높은 표준을 설정하고 소프트웨어 획득 및
개발을 통한 물리적 보안부터 직원 수명 주기 관리 및 보안 조직까지 종합적이고 전체적인 제어 목표 집합을
보유하고 있습니다. AWS 보안 글로벌 인프라 및 서비스는 정기적으로 타사 규정 준수 감사를 받아야 합니다.
자세한 내용은 Amazon Web Services 위험 및 규정 준수 백서를 참조하십시오. 

### IAM 서비스 

IAM 서비스는 본 백서에서 설명하는 AWS 보안 글로벌 인프라의 한 구성 요소입니다. IAM으로 사용자가 어떤 AWS
서비스와 리소스에 액세스할 수 있는지를 제어하는 암호, 액세스 키 및 사용 권한 정책과 같은 보안 자격 증명을
한 곳에서 관리할 수 있습니다.

AWS에 가입할 때 만든 AWS 계정에는 사용자 이름(이메일 주소)과 암호가 있어야 합니다. 사용자 이름과 암호로
AWS Management Console에 로그인해 브라우저 기반 인터페이스를 사용하여 AWS 리소스를 관리할 수 있습니다.
또한 액세스 키(액세스 키 ID와 보안 액세스 키로 구성)를 만들어 명령줄 인터페이스(CLI), AWS SDK 또는 API 호출로
AWS 프로그래밍 호출을 할 때 사용할 수 있습니다.


IAM을 사용하여 AWS 계정 내에 개별 사용자를 만들고 각 사용자에게 사용자 이름, 암호, 액세스 키를 부여할 수
있습니다. 개별 사용자는 계정별 URL을 사용하여 콘솔에 로그인할 수 있습니다. 또한 사용자별 액세스 키를
만들어 AWS 리소스에 액세스할 수 있도록 프로그래밍 호출을 할 수 있습니다. 고객의 IAM 사용자가 수행한
활동에 대한 모든 요금은 고객의 AWS 계정으로 청구됩니다. 자신이 사용할 IAM 사용자도 만들어 두고 일상적인
AWS 액세스에 AWS 계정 자격 증명을 사용하지 않는 것이 가장 좋습니다. 자세한 내용은 [IAM 모범 사례](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)를
참조하십시오.

### IAM 모범 사례

#### Lock away your AWS account(root) access keys 

AWS에 Programmatic request를 보내기 위해 access key를 사용할 수 있습니다. 하지만 AWS accound(root) access key를 사용하지 마십시오. AWS account access key는 청구 정보를 포함한 여러분의 모든 AWS 서비스에 대한 권한을 줍니다. AWS accound access key에 대한 권한을 제한할 수 없습니다.

그러므로 AWS accound access key를 신용카드 정보나 다른 예민한 비밀과 같이 보호하십시오. 이는 아래와 같은 방법으로 가능합니다.

* 만약 AWS account에 대한 access key가 없다면, 필요하다고 해도 만들지 마십시오. 대신에 account email 주소와 비밀번호를 이용하여 AWS Management Console에 로그인하여 당신의 관리 권한을 위한 IAM 계정을 만드십시오.
* 만약 AWS account 키가 있다면, 삭제하십시오. 만약 보관하고 있다면 주기적으로 변경해야합니다. 삭제나 변경을 위해서 [Security Credentials page](https://console.aws.amazon.com/iam/home?#security_credential)로 이동하여 관리하세요.
* AWS account 비밀번호나 access key를 다른 사람과 공유하지 마세요. 본 문서의 남은 섹션은다양한 방법으로 account 정보를 다른 사람과 안전하게 공유하고 application에 접근할 수 있게 하는지 다룰 것입니다.
* AWS Management Console에 대한 account 수준의 접근을 보호하기 위해 강력한 암호를 사용하십시오. [Changing the AWS Account("root") password](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_change-root.html)를 참고하십시오.
* AWS multifactor authentication(MFA)를 사용하세요. [Using Multi-Factor Authentication(MFA) in AWS](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)를 참고하십시오.

#### Create individual IAM users

AWS에 접근하기 위해 AWS root account를 사용하지 말고 다른 이에게 공유하지 마세요. 대신에 AWS 계정에 접근하기 위해 필요한 계정을 사용자별로 만드십시오. 관리자를 위한 IAM 사용자도 만들어야합니다. 

#### Use groups to assign permissions to IAM users

#### Grant least privilege

#### Configure a strong password policy for your users

#### Enable MFA for privileged users

#### Use roles for applications that run on Amazon EC2 instances

#### Delegate by using roles instead of by sharing credentials

#### Rotate crednetial regularly

#### Remove unnecessary credentials

#### Use policy conditions for extra security

#### Monitor activity in your AWS account



[http://d0.awsstatic.com/International/ko_KR/whitepapers/AWS_Security_Best_Practices_11052013.pdf](http://d0.awsstatic.com/International/ko_KR/whitepapers/AWS_Security_Best_Practices_11052013.pdf)

