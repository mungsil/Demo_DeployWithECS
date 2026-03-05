# ECS 실습

- 매 Step마다 기본 설정 설명은 생략한다.

# Prerequisites
- Cluster 생성, Task 정의

## [Step 1] ALB 생성

- 3가지 유의한다.

### 1. Availability Zone

<p align="center">
  <img width="330" height="248" alt="image" src="https://github.com/user-attachments/assets/c6d1b659-8eb9-4602-ae45-6cbb9bd9267b">
</p>

- ALB는 선택한 가용영역에 존재하는 resource로만 트래픽을 전달할 수 있다.  
- 따라서 앞으로 트래픽이 전달되기 원하는 리소스가 **여기서 선택한 가용 영역에 위치하는지** 고려해야 한다.

### 2. Security Group

<p align="center">
  <img width="627" height="231" alt="image" src="https://github.com/user-attachments/assets/8a673b22-c872-490e-b7e2-0afa0ca8c18a">
</p>

- ALB Security Group 설정 시 나는 ***ALB 전용 Security Group***을 만들어 Container가 해당 그룹에서 오는 트래픽만 받을 수 있도록 설정했다.

### 3. Target Group 
<p align="center"> 
  <img width="967" height="356" alt="image" src="https://github.com/user-attachments/assets/c8aa7b0d-4a69-42e2-992c-d18c5819015e" />
</p>
- type은 IP addresses를 선택한다. 


## [Step 2] ECS Service 생성
- 두 가지 유의한다.
  ### 1. Networking
  <p align="center">
    <img width="1119" height="673" alt="image" src="https://github.com/user-attachments/assets/eb117aa8-bc29-4934-89cc-3a474c3a70d4" />
  </p>
  - 가용영역: ALB에서 선택한 영역들
  - Security Group: 인바운드 포트는 컨테이너 포트, 소스는 ALB.
  <p align="center">
    <img width="1664" height="220" alt="image" src="https://github.com/user-attachments/assets/828aef54-317c-4e98-abc1-227631477357" />
  </p>
  
### 2. 로드밸런서 연결
<p align="center">
  <img width="1002" height="706" alt="image" src="https://github.com/user-attachments/assets/f48b7e84-52e9-4fd6-9855-53398cb7b4fb" />
</p>

### 끝.
- 서비스 생성 시 ALB 엔드포인트로 접근하면 서버 접근이 가능해진다.
## 참고 자료
- [유튜브](https://www.youtube.com/watch?v=o7s-eigrMAI)


