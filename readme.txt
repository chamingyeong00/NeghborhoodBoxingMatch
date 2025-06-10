README.txt

BoxingMatch Application 실행 가이드

이 문서는 연구실 컴퓨터 또는 로컬 환경에서 BoxingMatch Spring Boot 애플리케이션을 정상적으로 실행하기 위한 절차를 담고 있습니다.

==============================================================================
	1.	사전 요구 사항
==============================================================================

	•	운영체제: macOS 또는 Linux 배포판(Ubuntu, CentOS 등)
	•	Windows 환경인 경우 WSL2, Git Bash 또는 Cygwin 권장
	•	Java 17 JDK 설치
	•	OpenJDK 17 (LTS) 권장
	•	JAVA_HOME 환경 변수를 JDK 17 설치 경로로 설정
	•	PATH 에 $JAVA_HOME/bin 추가
	•	MySQL 8.x 설치
	•	데이터베이스 이름: boxing_match
	•	사용자: root
	•	비밀번호: 1234
	•	포트: 8080 (기본 Spring Boot 내장 Tomcat)

==============================================================================
2. 데이터베이스 준비
	1.	MySQL 서버 시작

sudo systemctl start mysql    # 또는 mysql.server start


	2.	MySQL에 접속

mysql -u root -p
# 비밀번호 입력: 1234


	3.	데이터베이스 및 사용자 권한 설정

CREATE DATABASE boxing_match CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
ALTER USER 'root'@'localhost' IDENTIFIED BY '1234';
FLUSH PRIVILEGES;
EXIT;



==============================================================================
3. 소스코드 준비
	1.	Git 레포지토리 클론

git clone https://github.com/chamingyeong00/NeghborhoodBoxingMatch.git
cd NeghborhoodBoxingMatch
cd BoxingMatch

	2.	Gradle Wrapper 실행 권한 부여 (macOS/Linux)

chmod +x gradlew



==============================================================================
4. 빌드 및 실행

4.1. 클린 빌드

./gradlew clean build

	•	실행 결과: BUILD SUCCESSFUL 메시지 확인
	•	생성 파일: build/libs/your-project-0.0.1-SNAPSHOT.jar

4.2. 개발 모드 실행

./gradlew bootRun

	•	콘솔에 Spring Boot 시작 로그 및 Tomcat 포트(8080) 확인

4.3. 패키징된 JAR 실행

java -jar build/libs/BoxingMatch-0.0.1-SNAPSHOT.jar \
  --spring.profiles.active=prod \
  --server.port=8080

==============================================================================
5. 실행 확인
	•	브라우저에서 http://localhost:8080 접속
	•	로그인 페이지, 매칭 등록/조회, 리뷰 작성 기능이 정상 동작하는지 확인
	•	건강 상태 확인 (Actuator)

curl -I http://localhost:8080/actuator/health
# HTTP/1.1 200 OK



==============================================================================
6. 주요 외부 라이브러리
	•	spring-boot-starter-web
	•	spring-boot-starter-data-jpa
	•	spring-boot-starter-thymeleaf
	•	spring-boot-starter-test
	•	com.mysql:mysql-connector-j
	•	org.projectlombok:lombok
	•	org.glassfish.jaxb:jaxb-runtime

==============================================================================
7. 문의 및 지원

문제 발생 시 로그를 첨부하여 개발자 또는 연구실 관리자에게 문의하세요.
