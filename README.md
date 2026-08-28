# GlobalGates 담당 기능 정리

GlobalGates 프로젝트에서 담당한 주요 서비스 기능을 정리한 포트폴리오 README입니다. 견적 요청, 전문가 대시보드, 전문가 요청 목록, 전문가 활동 목록, 관리자 페이지를 중심으로 화면과 서버 흐름을 연결했습니다.

## 프로젝트 링크

- 프로젝트 저장소: https://github.com/kausha-kr/globalgates
- 상세 포트폴리오: https://app.notion.com/p/3b2a62a7b858812e8e79c8604fc2e759
- 발표자료 이미지: https://github.com/kausha-kr/presentation/tree/main/assets/globalgates/slides

## 담당 서비스

### 1. 견적 요청 서비스

견적 요청 서비스는 사용자가 상품이나 무역 관련 업무에 대해 전문가에게 견적을 요청할 수 있는 기능입니다.

사용자는 요청 제목, 상세 내용, 마감일, 지역 등을 입력해 견적 요청을 등록할 수 있고, 전문가는 자신에게 들어온 견적 요청을 확인한 뒤 승인하거나 거절할 수 있습니다. 이 기능을 통해 사용자는 복잡한 무역 업무를 혼자 처리하지 않고 필요한 분야의 전문가에게 빠르게 상담과 견적을 요청할 수 있습니다.

**대표 코드**

```java
estimationDTO.setRequesterId(userDetails.getId());
estimationService.register(estimationDTO);
```

```java
estimationService.updateStatus(estimationId, "approve");
```

```javascript
const response = await fetch("/api/estimations", {
  method: "POST",
  headers: {"Content-Type": "application/json"},
  body: JSON.stringify(requestData)
});
```

### 2. 전문가 요약 페이지

전문가 요약 페이지는 전문가가 자신의 활동 현황을 한눈에 확인할 수 있는 대시보드입니다.

받은 견적 요청 수, 처리 상태, 최근 활동 내역을 한 화면에서 확인할 수 있도록 구성했습니다. 단순한 목록이 아니라 전문가가 오늘 확인해야 할 업무와 진행 중인 요청을 빠르게 파악하도록 돕는 화면입니다.

**대표 코드**

```javascript
const dashboard = await fetchJson("/api/inquiry/chart/dashboard");
renderDashboard(dashboard);
```

```javascript
google.charts.load("current", {
  packages: ["corechart", "geochart"]
});
```

```java
inquiryChartService.getDashboard(expertId);
```

### 3. 전문가 견적 요청 목록

전문가 견적 요청 목록은 전문가에게 들어온 견적 요청을 상태별로 확인할 수 있는 기능입니다.

요청 대기, 승인, 거절 등 상태에 따라 견적 요청을 구분하고, 각 요청의 상세 내용을 확인한 뒤 필요한 처리를 진행할 수 있도록 정리했습니다.

**대표 코드**

```java
estimationService.getReceivedRequests(expertId);
```

```java
estimationService.updateStatus(estimationId, status);
```

```javascript
const requests = await fetchJson(`/api/estimations/experts/${expertId}`);
renderRequestList(requests);
```

### 4. 전문가 활동 목록

전문가 활동 목록은 전문가와 관련된 사용자 활동을 확인할 수 있는 기능입니다.

전문가는 자신과 연결된 사용자, 최근 요청, 팔로우, 게시글 활동을 확인할 수 있습니다. 견적 요청만 처리하는 것이 아니라 플랫폼 안에서 어떤 사용자와 연결되고 있는지 파악할 수 있도록 돕습니다.

**대표 코드**

```java
followService.getSuggestions(memberId);
```

```java
activityService.getRecentActivities(expertId);
```

```javascript
const activities = await fetchJson("/api/inquiry/activities");
renderActivityList(activities);
```

### 5. 관리자 페이지

관리자 페이지는 서비스 운영자가 전체 서비스 현황을 관리할 수 있는 기능입니다.

회원, 게시글, 신고, 구독, 매출 예측 등 운영에 필요한 데이터를 한 화면에서 확인할 수 있도록 구성했습니다. 회원 상태 관리와 신고 콘텐츠 확인처럼 서비스 운영에 필요한 작업을 수행할 수 있습니다.

**대표 코드**

```javascript
const members = await adminService.getMembers();
renderAdminTable(members);
```

```javascript
const reports = await adminService.getReports();
renderReportTable(reports);
```

```java
adminService.updateMemberStatus(memberId, status);
```

## 구현 포인트

- Spring Boot와 MyBatis를 사용해 견적 요청, 전문가 페이지, 관리자 페이지 API 흐름을 정리했습니다.
- JavaScript fetch 기반으로 화면 데이터를 비동기로 조회하고, 목록과 차트를 동적으로 렌더링했습니다.
- 발표용 더미데이터를 구성해 견적 요청, 전문가 활동, 관리자 통계 화면을 실제 서비스처럼 확인할 수 있도록 준비했습니다.
- 화면 오류, 경로 오류, 이벤트 바인딩 누락, 외부 API 인증 문제를 원인별로 분리해 해결했습니다.

## 발표자료 이미지

![GlobalGates 발표자료 1](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-1.png)
![GlobalGates 발표자료 2](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-2.png)
![GlobalGates 발표자료 3](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-3.png)
![GlobalGates 발표자료 4](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-4.png)
![GlobalGates 발표자료 5](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-5.png)
![GlobalGates 발표자료 6](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-6.png)
![GlobalGates 발표자료 7](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-7.png)
![GlobalGates 발표자료 8](https://raw.githubusercontent.com/kausha-kr/presentation/main/assets/globalgates/slides/slide-8.png)
