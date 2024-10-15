# ◼︎ 카카오클라우드 VM 생성
### 클라우드를 이용하는 잇점 중 가장 좋은 것 중에 하나는 바로 즉시성 입니다.
#### 얼마나 빨리 새로운 서버를 만들 수 있는지 보여 드리도록 하겠습니다.
#### 무엇인가를 시도 하다 서버가 꼬이면 고민하지 마시고 다시 하시면 됩니다.

<br>
<br>
<br>
<br>
<br>

## 1. kakaocloud 콘솔 로그인
![image](https://github.com/user-attachments/assets/58d15e7c-d0eb-4b02-b4c3-547ab0cd70a3)

## 2. Virtual Machine 에 인스턴스 선택
![image](https://github.com/user-attachments/assets/5623ee90-d57c-4e40-ba9a-4c9cfdac8b2a)

## 3. 인스턴스 생성
### 1. 인스턴스 생성 버튼 클릭
![image](https://github.com/user-attachments/assets/ee570e6b-9045-4844-b6ef-cd53e0ca5587)
--
### 2. 서버명 입력 : lab-svr
![image](https://github.com/user-attachments/assets/2c4f6e72-b282-4686-b5f1-4eb32f39add0)
---
### 3. 이미지 선택 : Rocky_linux 9.4
![image](https://github.com/user-attachments/assets/deb41818-e72e-460a-82d0-5f8fc5cf7806)
---
### 4. 인스턴스 유형 : 컴퓨팅 최적화 , c2a.large
![image](https://github.com/user-attachments/assets/5be7d27a-ce08-4625-9b3a-46e36852d627)
---
### 5. 루트 볼륨 : 50GB
![image](https://github.com/user-attachments/assets/576700b7-2eec-4ddb-a294-d61280400dc1)
---
### 6. 키페어 : 앞 시간에 생성한 키페어 선택
![image](https://github.com/user-attachments/assets/3a7aeaf6-0d93-45a4-8dfc-34b11df5b2d3)
---
### 7. 네트워크

![image](https://github.com/user-attachments/assets/abeb2c6a-0197-49b1-80e4-35bfbe47f8e2)

- VPC : 앞전 실습에서 생성한 VPC 선택
- 서브넷 : main 서브넷 선택
- 보안그룹 : 아래와 같이 포트 오픈
  - 출발지 : www.naver.com 에서 "내 아이피 주소 확인" 으로 확인
  ![image](https://github.com/user-attachments/assets/9850df61-c501-4cc6-95ea-f9df88af79da)

![image](https://github.com/user-attachments/assets/e31f4ae3-5abf-440e-97c0-1118fe039bfa)
![image](https://github.com/user-attachments/assets/aeccbbe0-bd7b-4de2-bb2b-eb7f259750a1)
---
### 8. 생성 버튼 클릭

![image](https://github.com/user-attachments/assets/fd9d16e7-7480-4992-99b3-24fa6880c41e)
---
## 4. 공인 IP 생성 : VPC -> 퍼블릭 IP 선택
![image](https://github.com/user-attachments/assets/34b712ca-bd77-4434-8bd8-76781d1f1bf9)
---
#### "+ 퍼블릭 IP 생성" 클릭

![image](https://github.com/user-attachments/assets/9686dcec-ac50-499c-a9a3-311bc2772181)
---
#### 퍼블릭 IP 설명에 내용 입력(옵션)후  "생성" 버튼 클릭
![image](https://github.com/user-attachments/assets/e7ff0c5d-00d0-4ac0-b997-eaffe9ee5e9a)
---

#### 퍼블릭 IP 서버 연결 : 리소스 연결 선택
![image](https://github.com/user-attachments/assets/c311e2e6-5f04-4fba-9e77-1264609833a6)
---

#### 리소스 선택 : 앞에서 생성한 서버 선택 후 "저장" 버튼 클릭
![image](https://github.com/user-attachments/assets/5190b2ef-68d5-4af7-9c81-f169e5f44e9b)
---

<br>
<br>
<br>
<br>


# ◼︎ 주피터랩 설치 및 conda GATK 연동

## 1. System Update
패키지 업그레이드를 강제로 실행하면서 기존 의존성 문제를 무시하고 최신 버전으로 업데이트하는 옵션입니다.

sudo는 관리자 권한을 일시적으로 얻어 명령어를 실행하는 데 사용되는 유닉스 계열 운영체제에서의 명령어입니다. 주로 시스템 관리나 보안 관련 작업을 수행할 때 사용됩니다.
```
sudo dnf -y upgrade –refresh
```
시간대를 미국에서 한국으로 변경
```
sudo timedatectl
```
![image](https://github.com/user-attachments/assets/b12064be-9e70-4bc5-962e-90a3016d22e1)
```
sudo timedatectl set-timezone Asia/Seoul
```
![image](https://github.com/user-attachments/assets/ca40206a-2226-42c0-8518-724267d2700f)

#### 기본 repository 확인

```
sudo dnf repolist
```
Linux에서 Repository는 프로그램을 다운로드하고 설치 할 수 있는 저장소 입니다.

![image](https://github.com/user-attachments/assets/c4232c04-1c3d-4b52-8d9b-20ae314dd186)

위와 같이 기본적으로는 3개의 저장소가 활성화 되어 제공 됩니다. 제공되는 3개의 저장소에서 필요한 프로그램이 설치 되지 않을 수 있어 다음과 같이 저장소를 활성화 하거나 추가 합니다.

#### 모든 repository 확인

```
sudo dnf repolist all
```
![image](https://github.com/user-attachments/assets/03e68906-30c3-40b7-a7f1-ad2a68e3ce5d)


#### dnf config-manager 명령어는 CentOS Linux 8 이상 버전에서 제공되는 DNF(Dandified Yum) 패키지 매니저에서 사용되는 명령어이며 crb 패키지가 활성화되고, 
#### 이후 dnf update 또는 dnf upgrade 명령을 실행하면 crb 패키지가 설치됩니다.
```
sudo dnf config-manager --set-enabled crb
```
추가된 crb 레파지토리 확인
```
sudo dnf repolist
```
![image](https://github.com/user-attachments/assets/8cf154ba-3f50-4633-97ab-fdf4ef768bed)

![image](https://github.com/user-attachments/assets/3814184e-1ae3-401a-b5c8-be82fbfaca64)

#### RPM 추가 epel-next-release, epel-release
RPM(Red Hat Package Manager)은 레드햇 리눅스 계열 운영체제에서 사용되는 패키지 관리 도구입니다. 
RPM은 소프트웨어 패키지를 설치, 삭제, 업그레이드 및 유지보수하는데 사용됩니다.
```
sudo dnf -y install \
    https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm \
    https://dl.fedoraproject.org/pub/epel/epel-next-release-latest-9.noarch.rpm
```
#### noarch : 아키텍처 무관, CPU가 인텔이건 AMD건 관계 없이 설치 가능하다는 의미

추가된 레파지토리 확인
```
sudo dnf repolist
```
![image](https://github.com/user-attachments/assets/ced4eebf-2c39-4b83-8da7-7afe94ef4d96)

![image](https://github.com/user-attachments/assets/165b69a5-0568-4de1-81b4-688f479d5e47)

#### dnf -y update 명령은
- 기존에 설치된 패키지들의 최신 버전을 확인하고, 필요한 경우 최신 버전으로 업데이트합니다.
- 패키지 목록 데이터베이스를 갱신하여 최신 상태로 유지합니다.
1. dnf는 먼저 패키지 목록 데이터베이스를 조회하여 현재 설치된 패키지들의 최신 버전을 확인합니다.
2. 만약 최신 버전이 이미 설치되어 있다면 아무 작업도 하지 않고 종료됩니다.
3. 그렇지 않은 경우, 최신 버전의 패키지를 다운로드하고 설치합니다.
4. 이 과정에서 일부 패키지는 의존성 문제로 인해 설치되지 않을 수도 있습니다.
```
sudo dnf -y update
```

## 2. System Extension Install
wget, git-lfs net-tools traceroute 설치
```
sudo dnf -y install wget git-lfs net-tools traceroute
```
<br>

Development Tools 설치 -- 필요시 소스코드등을 컴파일 할때 필요..
```
sudo dnf -y groupinstall 'Development Tools'
```
위 명령어는 "개발 도구" 그룹에 속하는 모든 패키지를 자동으로 설치합니다.
설치 후에는 해당 패키지들을 사용하여 다양한 프로그래밍 작업을 수행할 수 있습니다. 예를 들어, Python, Java, C/C++, Go 등의 언어를 사용하여 프로그램을 개발할 수 있습니다. 또한, 디버깅 도구, 테스트 도구, 라이브러리 등도 함께 설치되므로 개발 작업을 더욱 효율적으로 수행할 수 있습니다. 그룹 패키지를 설치하면 여러 개의 개별 패키지를 일일이 설치하는 것보다 빠르고 간편합니다.

## 3. Environment-modules 설치
```
sudo yum -y install environment-modules
```

## 4. java 설치
```
sudo dnf -y install java-11-openjdk-devel java-17-openjdk-devel
```

## 5. miniconda 설치
```
sudo mkdir -p /opt/miniconda3
```
```
sudo chown -R 1000:1000 /opt/miniconda3
```
```
sudo chown -R rocky:rocky /opt/miniconda3
```
```
sudo wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /opt/miniconda3/miniconda.sh
```
```
sudo bash /opt/miniconda3/miniconda.sh -b -u -p /opt/miniconda3
```
```
sudo rm -rf /opt/miniconda3/miniconda.sh
```
```
/opt/miniconda3/bin/conda init bash
```
쉘을 빠져나왔다가 다시 들어가면 설치된 콘다 (base)환경으로 접속됩니다.

## 6. 콘다 채널 추가
채널 default, bioconda, conda-forge
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

등록 채널 확인
```
conda config --show channels
```

채널 우선 순위 변경
```
conda config --set channel_priority strict
```

## 7. jupyterlab 설치
```
conda install -y jupyterlab
```
설치 명령 이후 아래와 같이 쓰기 권한이 없다는 메시지가 나오면
![image](https://github.com/user-attachments/assets/ceae5328-9c79-47a5-affe-aac14a3a110b)

아래 명령을 다시 한번 수행 후,
```
sudo chown -R rocky:rocky /opt/miniconda3
```
주피터랩 설치 명령을 한번 더 수행
```
conda install -y jupyterlab
```
아래와 같이 모든 과정이 "done"으로 표기 되면 설치 완료!!!
![image](https://github.com/user-attachments/assets/3adb1315-15bc-400e-945f-a2d317755077)

## 8. 데이터시각화 라이브러리 bokeh extension 설치
```
conda install -y jupyter_bokeh
```
아래와 같이 모든 과정이 "done"으로 표기 되면 설치 완료!!!
![image](https://github.com/user-attachments/assets/b19891ef-6e90-4015-a578-a8eb6b796c08)

## 9. 아나콘다와 주피터랩의 가상환경을 연결해 주는 nb_conda_kernel 설치
```
conda install -y nb_conda_kernels
```
### 아래처럼 나오면 정상 설치!!!
![image](https://github.com/user-attachments/assets/1d479fad-257b-480e-a039-b09d0ce347bb)

#### 1. 편리한 주피터 노트북 사용
  - conda 환경을 쉽게 선택하고 전환할 수 있어 주피터 노트북을 더욱 편리하게 사용할 수 있습니다. 
#### 2. 에러 해결
  - DLL 임포트 에러 등의 문제를 해결할 수 있습니다.

## 10. 주피터랩 실행 확인
```
jupyter lab --ip=0.0.0.0 --port=8888 --allow-root --no-browser
```
- 옵션설명
  1. --ip=0.0.0.0 : 접근하는 모든 IP에 대해서 접속을 허용. 
  2. --port=8888 : 8888번 포트로 들어 오는 서비스만 허용
  3. --allow-root : root 권한을 가지고 실행 (윈도우에 관리자 권한으로 실행과 유사)
  4. --no--browser : 브라우저를 띄우지 마라
     
![image](https://github.com/user-attachments/assets/f4ae0f8b-155a-40b7-bef4-58b9e19a5835)

## 11.포트에 대한 개념과 방화벽에 대한 개념

![image](https://github.com/user-attachments/assets/ece4e3f6-e754-4edb-bc19-712c788a883e)

## 12. GATK conda 설치
(base) 환경에서 설치 <br>

![image](https://github.com/user-attachments/assets/aa19b3ac-7c32-4bc7-b8b7-a04302e1ec24)

### gatk 가상환경 생성
```
conda create -y -n gatk
```

![image](https://github.com/user-attachments/assets/aa3d417c-ed92-44cc-b28b-8c22791b7592)

### gatk 가상환경으로 진입
```
conda activate gatk
```
![image](https://github.com/user-attachments/assets/9eeb679b-6b13-4de0-8082-d79e838309cb)

### python version 확인
```
python -V
```

### 채널 우선 순위 변경
```
conda config --set channel_priority flexible
```
flexible 모드에서는 각 채널의 최신 버전 패키지가 자동으로 선택됩니다. 이 모드는 안정적인 패키지보다는 최신 버전의 패키지를 선호하는 경우에 유용합니다.

•	strict: 공식 채널의 패키지를 우선적으로 선택합니다.

•	relaxed: 공식 채널과 비공채널의 패키지를 동등하게 고려합니다.

•	flexible: 각 채널의 최신 버전 패키지를 자동으로 선택합니다.

<br>
<br>
<br>
<br>


# ◼︎ conda gatk 환경에 각종 툴 설치
## install bwa, vcfstats, vcftools, bedtools, fastqc, somalier, slivar, salmon, s5cmd, plink, plink2, multiqc, minimap2, htslib, king, libxml2-devel-cos6-x86_64, gistic2 설치

## 1. 10x_bamtofastq 설치
```
conda install -y bioconda::10x_bamtofastq
```
### 설치확인
```
bamtofastq
```

![image](https://github.com/user-attachments/assets/f228174d-4928-4cfc-993b-ce432fde42db)

## 2. ctat-mutations 설치
```
conda install bioconda::ctat-mutations
```
주피터랩 연동 확인
1. (base) 환경에서 주피터랩 실행   
2. gatk 가상환경 아이콘 확인 <br>

![image](https://github.com/user-attachments/assets/5a6735dc-59d0-479a-85f7-94e3243c7fa3)

3. gatk 명령어 실행 확인 - 주피터랩에서 외부명령 실행시 명령어 앞에 "느낌표" + 실행하고자하는 명령어 ! <br>
```
!gatk
```
![image](https://github.com/user-attachments/assets/8341da54-b8e5-408a-9e00-48d6cb7834ab)


## 3. bwa 설치
```
conda install -y bioconda::bwa
```
### 설치확인
```
bwa
```

![image](https://github.com/user-attachments/assets/383380de-de05-4561-832b-2b39f441d883)


## 3. biopet-vcfstats 설치
```
conda install -y bioconda::biopet-vcfstats
```

### 설치확인
```
biopet-vcfstats
```

![image](https://github.com/user-attachments/assets/6cd4b92d-d4cf-4b95-b358-a8f0663f71a1)

## 4. vcftools 설치
```
conda install -y bioconda::vcftools
```
### 설치확인
```
vcftools
```

![image](https://github.com/user-attachments/assets/6b358e08-a66c-4561-9b91-041413c4efae)

## 5. bedtools 설치
```
conda install -y bioconda::bedtools
```
### 설치확인
```
bedtools
```

![image](https://github.com/user-attachments/assets/02536580-5059-4c78-ac5b-6615c66fa89b)

## 6. fastqc 설치
```
conda install -y bioconda::fastqc
```
### 설치확인
```
fastqc
```

![image](https://github.com/user-attachments/assets/22305c63-c670-47e7-b0ad-0826ce2b6ff4)


## 7. somalier 설치
```
conda install -y bioconda::somalier
```
### 설치확인
```
somalier
```

![image](https://github.com/user-attachments/assets/17196aa4-9877-45c6-9f9f-ef0abb7c5ed0)

## 8. slivar 설치
```
conda install -y bioconda::slivar
```
### 설치확인
```
slivar
```

![image](https://github.com/user-attachments/assets/52b4f9a4-62e8-4e1e-9341-20aa1e156f2a)

## 9. salmon 설치
```
conda install -y salmon
```
### 설치확인
```
salmon
```

![image](https://github.com/user-attachments/assets/d4ff2913-27fe-426c-a7b9-51e84e94e34c)

## 10. s5cmd 설치
```
conda install -y conda-forge::s5cmd
```
### 설치확인
```
s5cmd
```

![image](https://github.com/user-attachments/assets/42204e82-af72-4a25-a0a4-7ca76d47cfb4)

## 11. plink 설치
```
conda install -y bioconda::plink
```
### 설치확인
```
plink
```

![image](https://github.com/user-attachments/assets/58d32fd9-becc-45ee-a18c-f93396b18543)

## 12. plink2 설치
```
conda install -y bioconda::plink2
```
### 설치확인
```
plink2
```

![image](https://github.com/user-attachments/assets/432dc555-12a9-4e8c-a76f-6d848586b813)

## 13. multiqc 설치 ★
```
conda install -y bioconda::multiqc
```
### 설치확인
```
cd /opt/miniconda3/envs/gatk/bin
```

![image](https://github.com/user-attachments/assets/43fbc731-d747-45e8-8059-7eb56c48c713)

```
cd
```

## 14. minimap2 설치
```
conda install -y bioconda::minimap2
```
### 설치확인
```
minimap2
```

![image](https://github.com/user-attachments/assets/2f7763bb-ffe1-43e3-a36a-f7e73a009d1a)


## 15. king 설치
```
conda install -y bioconda::king
```
### 설치확인
```
king
```

![image](https://github.com/user-attachments/assets/46e7a5e8-7716-44ee-98e2-e1278de9775f)


## 16. libxml2-devel-cos6-x86_64 설치
```
conda install -y conda-forge::libxml2-devel-cos6-x86_64
```
### 설치확인
```
k8
```

![image](https://github.com/user-attachments/assets/e71f64c4-8e33-4498-a553-0a50c8bb99fb)

## 17. gistic2 설치 ★
```
conda install -y hcc::gistic2
```
### 설치확인
```
gistic2
```
### 라이브러리 없다는 오류 나오면 아래 명령 실행

![image](https://github.com/user-attachments/assets/fdcf6247-dd06-4e76-a1ca-96747c4eae66)

```
sudo ln -s /usr/lib64/libncursesw.so.6.2 /usr/lib64/libncurses.so.5
sudo ln -s /usr/lib64/libncursesw.so.6.2 /usr/lib64/libtinfo.so.5
sudo ln -s /usr/lib64/libform.so.6.2 /usr/lib64/libform.so.5
```

## 18. bioconductor-mafdb.gnomadex.r2.1.hs37d5 설치 ★
```
conda install -y bioconda::bioconductor-mafdb.gnomadex.r2.1.hs37d5
```
### 설치확인
```

```

![image](https://github.com/user-attachments/assets/b83299a6-931a-415d-999f-7bc83edf0c90)


## 19. bioconductor-mafdb.gnomadex.r2.1.grch38 설치
```
conda install -y bioconda::bioconductor-mafdb.gnomadex.r2.1.grch38
```
### 설치확인
```
yq
```

## 20.Rust 설치

![image](https://github.com/user-attachments/assets/cc83dce7-692f-4624-a42d-7880b2274aa1)

### 공식 홈페이지에 있는 설치 명령어 ★
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
[Install Rust 공식 홈페이지](https://www.rust-lang.org/tools/install)

### 쉘 반영
```
source $HOME/.cargo/env
```

### 파일 편집
```
cat << EOF > hello.rs
fn main() {
        println!("안녕하세요! 여기는 생명정보학회 경주 입니다.");
}
EOF
```
### 컴파일
```
rustc hello.rs
```
### 결과 파일 확인
```
ls -lrt
```

![image](https://github.com/user-attachments/assets/59b9dbf9-161e-49af-b772-b61eb6fb0248)

### hello 실행
```
./hello
```

![image](https://github.com/user-attachments/assets/dccad5c1-7baf-4a0d-affd-5f8db49110ec)

## 21. rtoml 설치
```
pip install rtoml
```

## 22. vcfstats 설치 ★
```
pip install -U vcfstats
```
[vcfstats 공식 홈페이지](https://pwwang.github.io/vcfstats/)


![image](https://github.com/user-attachments/assets/29f75b3d-6e2b-48a7-a039-41ad1c629adf)


## 23. JAVA 실행 환경 변경

### java 버전 확인
```
java -version
```
![image](https://github.com/user-attachments/assets/599972b4-c9f6-4de6-b7b5-6d54e3feb08b)

### 설치된 자바 삭제
```
sudo rm /opt/miniconda3/envs/gatk/bin/java
```
### 시스템에 설치된 자바로 연결
```
sudo ln -s /usr/bin/java /opt/miniconda3/envs/gatk/bin/java
```
![image](https://github.com/user-attachments/assets/e37bb0b5-deb0-49d1-92fe-f681b9c467db)

### java 버전 변경
```
sudo alternatives --config java
```
![image](https://github.com/user-attachments/assets/085d8640-8550-4d1b-a634-4f4d97c98588)

## 24. 주피터랩과 gatk 환경 연동
```
conda install anaconda::ipykernel
```

## 25. 가상환경 빠져나오기
```
conda deactivate
```

<br>
<br>
<br>
<br>


# ◼︎ manta conda 설치
## 1. manta 가상환경 생성
```
conda create -y -n manta python=2.7
```
## 2. manta 가상환경 진입
```
conda activate manta
```
## 3. 파이썬 버전 2.7 확인
```
python -V
```
## 4. manta 설치
```
conda install -y bioconda::manta
```
## 5. strelka 설치
```
conda install -y bioconda::strelka
```
## 6. 주피터랩과 gatk 환경 연동
```
conda install anaconda::ipykernel
```
## 7. pip 재설치
```
pip 
```
![image](https://github.com/user-attachments/assets/fb98af70-ada3-4c57-9fee-cf1a401a9ff2)

위와 같이 에러 발생하면...

### pip 2.7용 소스 가져오기
```
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
```
### pip 재설치
```
python get-pip.py
```

![image](https://github.com/user-attachments/assets/ac5933c9-54d7-4615-8b48-850146085104)

### pip 실행확인
```
pip -V
```

![image](https://github.com/user-attachments/assets/51aee903-c4d3-4f87-b231-5bb406f86706)

## 8. 가상환경 빠져나오기
```
conda deactivate
```


<br>
<br>
<br>
<br>





# ◼︎ hail conda 설치
## 1. hail 가상환경 생성
```
conda create -y -n hail python=3.10
```
## 2. hail 가상환경 진입
```
conda activate hail
```
## 3. 파이썬 버전 2.7 확인
```
python -V
```
## 4. hail 설치
```
pip install hail
```
## 5. colabfold 설치
```
conda install -y bioconda::colabfold
```
## 6. crossmap 설치
```
conda install -y bioconda::crossmap
```
## 7. deeptools 설치
```
conda install -y bioconda::deeptools
```
## 8. harfbuzz 설치
```
conda install -y conda-forge::harfbuzz
```
## 9. liftover 설치
```
conda install -y bioconda::liftover
```
## 10. postgresql-devel 설치
```
sudo dnf install -y postgresql-devel
```
## 11. psycopg2 설치
```
pip install psycopg2
```
## 12. gnomad 설치
```
pip install gnomad
```
## 13. 주피터랩과 gatk 환경 연동
```
conda install anaconda::ipykernel
```
### 연동 확인
![image](https://github.com/user-attachments/assets/c4fe0fcc-3f13-419f-943b-d73ff7839a6a)


<br>
<br>
<br>
<br>



# ◼︎ DeNovoCNN 설치
## 1. 디렉토리 홈으로 이동
```
cd
```
## 2. git에서 소스 가져오기
```
git clone https://github.com/Genome-Bioinformatics-RadboudUMC/DeNovoCNN.git
```
## 3. 디렉토리 이동
```
cd ./DeNovoCNN
```
## 4. 채널 우선순위 변경
```
conda config --set channel_priority flexible
```
flexible 모드에서는 각 채널의 최신 버전 패키지가 자동으로 선택됩니다. 

이 모드는 안정적인 패키지보다는 최신 버전의 패키지를 선호하는 경우에 유용합니다.

•	strict: 공식 채널의 패키지를 우선적으로 선택합니다.
•	relaxed: 공식 채널과 비공채널의 패키지를 동등하게 고려합니다.
•	flexible: 각 채널의 최신 버전 패키지를 자동으로 선택합니다.

## 5. yml파일을 이용한 콘다 가상환경 생성 및 패키지 설치
```
conda env create -f environment.yml
```

![image](https://github.com/user-attachments/assets/9d4ad80c-d1a9-4d35-be09-89a46a095e17)

## 6. 가상환경으로 진입
```
conda activate tensorflow_env
```

## 7. ipykernel 설치
```
conda install anaconda::ipykernel
```

## 8. 주피터랩 확인

![image](https://github.com/user-attachments/assets/5f3f14e2-60ce-46e0-b1e0-50f0a2071dc2)

![image](https://github.com/user-attachments/assets/77680e65-9e2b-46cc-a0d7-61d2adc27371)

- Collecting asttokens==2.0.5
- Collecting backcall==0.2.0
- Collecting decorator==5.1.1
- Collecting executing==0.8.3
  
..

..

..


<br>
<br>
<br>
<br>



# ◼︎ annotsv conda 설치
## 1. annotsv 가상환경 생성
```
conda create -y -n annotsv
```
## 2. annotsv 가상환경 진입
```
conda activate annotsv
```
## 3. 파이썬 버전 2.7 확인
```
python -V
```
## 4. annotsv 설치
```
conda install -y bioconda::annotsv
```
## 5. 주피터랩과 annotsv 환경 연동
```
conda install anaconda::ipykernel
```
## 6. annotsv conda deactivate
```
conda deactivate
```

<br>
<br>
<br>
<br>

# ◼︎ Triodenovo 설치

## 1. 홈 디렉토리 이동
```
cd
```
```
pwd
```
![image](https://github.com/user-attachments/assets/9a4022d5-5c2e-4867-933b-3f36b221bf05)

## 2.파일 다운로드
```
wget --no-check-certificate https://genome.sph.umich.edu/w/images/f/f4/Triodenovo.0.06.tar.gz
```

## 3.파일 압축해제
```
tar -xzvf Triodenovo.0.06.tar.gz
```

## 4.다운로드 한 압축파일 삭제
```
rm -f Triodenovo.0.06.tar.gz
```

## 5.디렉토리 이동
```
cd ./triodenovo.0.06/base
```

## 6.Argument.h 파일 수정
- 변경 전
![image](https://github.com/user-attachments/assets/a1865a6c-4a33-467a-9195-037278aa351f)

```
sed -i '366 c\                 if (strcmp(argv[i+1], "") == 0) {' Argument.h
```
- 변경 후
![image](https://github.com/user-attachments/assets/9cd0be1d-98a0-4277-a7c7-05173f6fa3d3)

## 7.디렉토리 이동
```
cd ../core
```

## 8.Parameters.cpp 파일 수정
- 변경 전
  
![image](https://github.com/user-attachments/assets/1176a7a9-fb1f-49fd-aab8-f3122c9b344e)

```
sed -i '501s/bool/int/g' Parameters.cpp
```
- 변경 후
  
![image](https://github.com/user-attachments/assets/f9c3c9a3-e832-4831-8bc1-881a3e88e387)

## 9.디렉토리 이동
```
cd ..
```

## 10.make
make에 필요한 툴 설치
```
sudo dnf install bzip2-devel
```
```
make
```

## 11.결과 메시지 확인

![image](https://github.com/user-attachments/assets/34fdb5ef-b330-4d52-88cc-ff91d6ff2f26)

## 12.실행파일 확인

```
cd bin
```
```
./triodenovo
```

![image](https://github.com/user-attachments/assets/9c0b3312-ac2a-4341-8da5-78a0805c2a3c)

## 13.디렉토리 등록
```
echo 'export PATH=$PATH:/home/rocky/triodenovo.0.06/bin' >> ~/.bashrc
```
## 14.쉘 재기동
### 홈디렉토리 이동
```
cd
```
### 쉘 반영
```
source ~/.bashrc
```
### 프로그램 실행 확인
```
triodenovo
```

<br>
<br>
<br>
<br>



# ◼︎ dSQ 설치

## 1. 홈디렉토리 이동
```
cd
```
## 2. git에서 내려받기
```
git clone https://github.com/ycrc/dSQ.git
```

<br>
<br>
<br>
<br>


# ◼︎ eigensoft 설치

## 1. 홈디렉토리 이동
```
cd
```
## 2. git에서 내려받기
```
git clone https://github.com/argriffing/eigensoft.git
```
## 3. 압축파일 해제
```
unzip v7.0.2.zip
```
## 4. 디렉토리 이동
```
cd eigensoft/src
```
## 5. make
```
make eigenstrat
```
## 6. 실행파일 이동
```
mv eigenstrat ../bin
```

<br>
<br>
<br>
<br>



# ◼︎ AdmixTools 설치

## 1.설치 위치
```
cd
```
```
pwd
```

![image](https://github.com/user-attachments/assets/50c776f5-de4c-40f4-9506-0f90ab888c33)


## 2.소스 다운로드
```
wget https://github.com/DReichLab/AdmixTools/archive/refs/tags/v7.0.2.zip
```

## 3.컴파일에 필요한 툴 설치
```
sudo dnf install -y gsl-devel openblas-devel
```

## 4.파일 압축 해제
```
unzip v7.0.2.zip
```

## 5. 디렉토리 이동
```
cd ./AdmixTools-7.0.2/src
```

## 6.make
```
make clobber
```
```
make all
```
```
make install
```

## 7.압축파일 삭제
```
cd
```
```
rm -f v7.0.2.zip
```

## 8.프로그램 확인
```
cd AdmixTools-7.0.2/bin
```
```
ls -lrt
```
![image](https://github.com/user-attachments/assets/240bd318-7e73-410e-be8f-21d3a14cfdaa)

## 9.실행 디렉토리 등록
```
cd
```
```
echo 'export PATH=$PATH:/home/rocky/AdmixTools-7.0.2/bin' >> ~/.bashrc
```
### 쉘 반영
```
source ~/.bashrc
```
### 프로그램 실행 확인
```
dof4
```

<br>
<br>
<br>
<br>


# ◼︎ conda R 설치

## 1.가상환경 생성
```
conda create -y -n r_env python=3.10
```

## 2.가상환경 진입
```
conda activate r_env
```

## 3. 주피터랩과 rstudio 환경 연동
```
conda install anaconda::ipykernel
```

## 4. rstudio 설치
```
conda install -y r::rstudio
```

## 5. r-facets 설치
```
conda install -y bioconda::r-facets
```

## 6. 서버 재부팅
```
sudo reboot
```

## 7. 주피터랩에서 R 명령어 확인
```
str1 <- paste('Hello!', 'world!', 'is', 'good')
```
```
paste(str1)
```
```
available.packages()
```

![image](https://github.com/user-attachments/assets/242e1df9-0de2-4f11-9923-a66f63d3ce16)


<br>
<br>
<br>



# ◼︎ R Server 설치
## 1. R 설치
```
sudo dnf install -y R
```
## 2. RServer 설치
### 설치 파일 다운로드
```
wget https://download2.rstudio.org/server/rhel9/x86_64/rstudio-server-rhel-2024.09.0-375-x86_64.rpm
```
### RStudio 설치
```
sudo yum install rstudio-server-rhel-2024.09.0-375-x86_64.rpm
```
### RStudio 설치파일 삭제
```
rm -f rstudio-server-rhel-2024.09.0-375-x86_64.rpm
```
### rstudio-server 상태 확인
```
systemctl status rstudio-server
```
### 서비스 포트 확인
```
sudo netstat -nltp
```

![image](https://github.com/user-attachments/assets/acb1714b-b51b-468b-a579-d26f17733047)


## 5. SELinux 설정 및 rocky 비밀번호 생성

### 디렉토리 이동
```
cd /etc/selinux
```

### config 파일 수정
```
sudo sed -i '22s/SELINUX=enforcing/SELINUX=disabled/g' config
```
SELinux 를 해제후 다시 켤 경우 relabel이 필요하며 이때 잘못된 설정이 있을 경우 부팅이 안 되거나 ssh 로 원격 접속이 불가능할 수 있으므로 **enforcing** 모드가 아닌 **permissive** 모드로 설정 후 재부팅하는 것을 권장


### 파일 수정 확인
```
cat config
```
![image](https://github.com/user-attachments/assets/673ecf76-eace-4186-9e5d-7d23c68c4c4a)


### rocky 계정 비밀 번호 생성
```
sudo passwd rocky
```
원하는 비밀번호 입력 후 비밀번호 확인하여 등록

![image](https://github.com/user-attachments/assets/d133a5a7-8c0c-4107-aedf-fc93a5fc4d4b)

## 6. 서버 리부팅
```
sudo reboot
```

## 7. 서비스 접속

서버공인IP:8787
http://210.109.54.95:8787

![image](https://github.com/user-attachments/assets/d4f3536b-73c5-4163-a540-13678f2f3a97)

ID  : rocky

PWD : 위에서 지정한 비밀번호

![image](https://github.com/user-attachments/assets/99d90262-5b90-4a73-802e-38c3ba35fa93)

## 8. 홈 디렉토리로 이동
```
cd
```

<br>
<br>


# ◼︎ screen 설치
## 1. 설치
```
sudo yum install -y screen
```
## 2. 설치확인
```
screen -v
```
## 3. 홈 디렉토리로 이동
```
cd
```


<br>
<br>
<br>
<br>



# ◼︎ icav2-cli-plugins 설치

## 1. yq 설치
```
sudo wget https://github.com/mikefarah/yq/releases/download/v4.18.1/yq_linux_amd64 -O /usr/bin/yq
```

## 2. yq 실행모드 변경
```
sudo chmod +x /usr/bin/yq
```

## 3. awscli curl jq python3 rsync 설치
```
sudo dnf install -y awscli curl jq python3 rsync
```

## 4. conda gh 설치
```
conda install -y conda-forge::gh
```

## 5. awscliv2.zip 다운로드
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

## 6. awscliv2.zip 압축해제
```
unzip awscliv2.zip
```

## 7. aws cli 설치
```
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli–update
```

## 8. 압축파일 삭제
```
rm -rf awscliv2.zip
```

## 9. icav2-cli-plugins.git 다운로드
```
git clone https://github.com/umccr/icav2-cli-plugins.git
```

## 10. 디렉토리 이동
```
cd ./icav2-cli-plugins/
```

## 11. 설치명령어 수행
```
sh install.sh
```

## 12. 홈 디렉토리로 이동
```
cd
```

## 13. .bashrc 파일 수정
```
echo '. "${HOME}/.icav2-cli-plugins/source.sh"' | tee -a .bashrc
```

## 14. .bashrc 다시 실행
```
source ~/.bashrc
```

<br>
<br>
<br>
<br>


# ◼︎ conda docker 설치

## 1. 홈 디렉토리로 이동
```
cd
```

## 2. docker-compose 설치
```
conda install -y conda-forge::docker-compose
```

## 3. docker-py 설치
```
conda install -y conda-forge::docker-py
```

## 4. docker 설치
```
sudo dnf install -y docker
```

<br>
<br>
<br>
<br>



# ◼︎ Galaxy 설치
## 1.SSH 서버 접속 및 위치 확인

![image](https://github.com/user-attachments/assets/18b2480a-b6b6-4818-8716-4ec4260f6cea)

(base) 가상환경 확인

![image](https://github.com/user-attachments/assets/05f59f13-1eff-441a-94d8-b48c9c95b789)

(base) 디렉토리 위치 확인 <br>
```
pwd
```
![image](https://github.com/user-attachments/assets/d9c9a7a9-fcf1-4083-be9c-a52cf463072d)

## 2.소스 다운로드
```
git clone https://github.com/galaxyproject/galaxy.git
```
## 3.다운받은 디렉토리로 이동
```
cd ./galaxy
```

## 4.소스 Update
```
git fetch origin && git checkout release_24.1 && git pull --ff-only origin release_24.1
```

## 5.설치
```
sh run.sh
```

# ◼︎ 외부에서 galaxy 접속을 위한 설정
최초에 galaxy를 설치하면 내부에서만 접속이 가능한 상태로 실행이 됩니다.

![image](https://github.com/user-attachments/assets/1416d4e5-38bd-4872-923e-4d4aff207792)

여기에서 Serving on http://127.0.0.1:8080 이 부분을 외부에서 접속이 가능하도록 0.0.0.0:8080 으로 변경합니다.
## 1.서비스 종료
control + c 를 이용하여 갤럭시 웹서비스를 종료 합니다.

## 2.config 변경을 위해 디렉토리 이동
```
cd /home/rocky/galaxy/config
```

## 3.원본 config 파일 복사
```
cp galaxy.yml.sample galaxy.yml
```

## 4.galaxy.yml 파일 수정
```
sed -i '92s/localhost/0.0.0.0/g' galaxy.yml
```
```
sed -i '92s/#/ /g' galaxy.yml
```

![image](https://github.com/user-attachments/assets/61b32fe5-85cb-4573-b908-7a847a9a929a)


## 5.galaxy.yml 파일 저장
gunicorn : 웹 서버로 부터 받은 요청을 웹 어플리케이션에 전달해 주는 역할을 함.

웹서버의 설정을 나자신에서 모든 서버의 요청을 받을 수 있도록 변경하는 작업임.

## 6.실행 디렉토리로 이동
```
cd ..
```

## 7.galaxy 다시 실행
```
sh run.sh
```

## 8. 0.0.0.0:8080 으로 서비스가 실행 되었는지 확인
```
sudo netstat -nltp
```

![image](https://github.com/user-attachments/assets/66ac0e5b-57d9-4c94-a940-fc0a9cd1656e)


## 9.브라우저 접속 URL에 자신의 서버공인 IP를 입력 후 8080포트로 접속 확인
크롬등의 브라우저 창을 열고 주소란에 입력 http://210.109.54.95:8080

![image](https://github.com/user-attachments/assets/0e6c827a-337d-4432-bdc4-b01ea62e8490)


<br>
<br>
<br>
<br>


# ◼︎ Only GATK 설치 및 실행

## 1. wget, unzip 설치
```
sudo dnf -y install wget unzip
```

## 2. java17 설치
```
sudo dnf -y install java-17-openjdk-devel
```

## 3. GATJ 설치 파일 다운로드
```
wget https://github.com/broadinstitute/gatk/releases/download/4.6.0.0/gatk-4.6.0.0.zip
```

## 4. 압축해제
```
unzip gatk-4.6.0.0.zip
```

## 5. 압축파일 삭제
```
rm -rf gatk-4.6.0.0.zip
```

## 6. 쉘파일 수정
```
echo 'export PATH=$PATH:{path} /gatk-4.6.0.0' >> ~/.bashrc
```

## 7. 쉘파일 재시동
```
source ~/.bashrc
```

## 8. GATK 명령 옵션 예시
```
gatk BaseRecalibrator \
   -I dedup.NA12878.bam \
   -R hs38DH.fasta \
   --known-sites dbsnp_146.hg38.vcf.gz \
   --known-sites 000G_phase1.snps.high_confidence.hg38.vcf.gz \
   --known-sites Mills_and_1000G_gold_standard.indels.hg38.vcf.gz \
   -O NA12878.recal.table
```




