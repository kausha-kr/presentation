## 담당 서비스

### 1. 견적 요청 서비스

견적 요청 서비스는 사용자가 상품이나 무역 관련 업무에 대해 전문가에게 견적을 요청할 수 있는 기능입니다.

사용자는 요청 제목, 상세 내용, 마감일, 지역 등을 입력해 견적 요청을 등록할 수 있습니다.  
전문가는 자신에게 들어온 견적 요청을 확인하고, 요청 내용을 검토한 뒤 승인하거나 거절할 수 있습니다.

이 기능을 통해 사용자는 복잡한 무역 업무를 혼자 처리하지 않고, 필요한 분야의 전문가에게 빠르게 상담과 견적을 요청할 수 있습니다.

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

---

### 2. 전문가 요약 페이지

전문가 요약 페이지는 전문가가 자신의 활동 현황을 한눈에 확인할 수 있는 대시보드입니다.

전문가는 받은 견적 요청 수, 처리 상태, 최근 활동 내역 등을 한 화면에서 확인할 수 있습니다.  
이를 통해 오늘 어떤 요청을 확인해야 하는지, 어떤 업무가 진행 중인지 빠르게 파악할 수 있습니다.

이 페이지는 단순한 목록이 아니라 전문가의 업무 흐름을 요약해서 보여주는 역할을 합니다.

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

---

### 3. 전문가 견적 요청 목록

전문가 견적 요청 목록은 전문가에게 들어온 견적 요청을 상태별로 확인할 수 있는 기능입니다.

전문가는 요청 대기, 승인, 거절 등 상태에 따라 견적 요청을 구분해서 볼 수 있습니다.  
각 요청의 상세 내용을 확인한 뒤 필요한 처리를 진행할 수 있습니다.

이 기능을 통해 전문가는 고객이 보낸 요청을 놓치지 않고 체계적으로 관리할 수 있습니다.

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

---

### 4. 전문가 활동 목록

전문가 활동 목록은 전문가와 관련된 사용자 활동을 확인할 수 있는 기능입니다.

전문가는 자신과 연결된 사용자, 최근 요청, 팔로우, 게시글 활동 등을 확인할 수 있습니다.  
이를 통해 플랫폼 안에서 어떤 사용자와 연결되고 있는지, 어떤 활동이 발생하고 있는지 파악할 수 있습니다.

이 기능은 전문가가 견적 요청만 처리하는 것이 아니라 자신의 네트워크와 활동 흐름을 함께 확인할 수 있도록 돕습니다.

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

---

### 5. 관리자 페이지

관리자 페이지는 서비스 운영자가 전체 서비스 현황을 관리할 수 있는 기능입니다.

관리자는 회원, 게시글, 신고, 구독, 매출 예측 등 운영에 필요한 데이터를 한 화면에서 확인할 수 있습니다.  
회원 상태를 관리하거나 신고된 콘텐츠를 확인하는 등 서비스 운영에 필요한 작업을 수행할 수 있습니다.

이 페이지를 통해 관리자는 서비스 전체 흐름을 빠르게 파악하고 안정적으로 운영할 수 있습니다.

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
---


## 구현 포인트

- Spring Boot와 MyBatis를 사용해 견적 요청, 전문가 페이지, 관리자 페이지 API를 구현했습니다.
- JavaScript를 사용해 화면 데이터를 비동기로 조회하고, 목록과 차트를 동적으로 렌더링했습니다.
- 발표용 더미데이터를 구성해 견적 요청, 전문가 활동, 관리자 통계 화면을 실제 서비스처럼 확인할 수 있도록 준비했습니다.
