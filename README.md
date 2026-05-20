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

## AI 서비스

### 1. 견적 요청 AI 검토

견적 요청 AI 검토는 사용자가 견적 요청을 작성할 때, AI가 요청 내용을 자동으로 분석하는 기능입니다.

AI는 사용자가 입력한 제목과 내용을 바탕으로 해당 글이 견적 요청으로 적절한지 판단합니다.  
내용이 너무 짧거나 의미가 부족한 경우에는 사용자가 다시 작성할 수 있도록 도와줍니다.

이를 통해 잘못 작성된 요청이나 의미 없는 요청을 줄이고, 전문가가 더 정확한 견적 요청을 받을 수 있도록 했습니다.

**대표 코드**

```javascript
const result = await service.classifyEstimation(title, content);
```

```java
webClient.post()
    .uri("/estimation/estimation-regist")
    .bodyValue(request);
```

```python
@app.post("/estimation/estimation-regist")
def predict_estimation(request: ClassificationRequest):
    return classify(request)
```

---

### 2. 전문가 추천 AI

전문가 추천 AI는 사용자의 정보와 관심 분야를 바탕으로 적절한 전문가를 추천하는 기능입니다.

사용자의 지역, 관심 카테고리, 태그 정보를 분석해 관련성이 높은 전문가를 우선적으로 보여줍니다.  
사용자는 직접 전문가를 일일이 찾지 않아도 자신에게 맞는 전문가를 쉽게 확인할 수 있습니다.

이 기능은 사용자와 전문가를 더 빠르게 연결하기 위해 구현했습니다.

**대표 코드**

```java
webClient.post()
    .uri("/recommendation/experts")
    .bodyValue(request);
```

```javascript
const experts = await loadAiExperts(memberId);
renderAiExperts(experts);
```

```python
@app.post("/recommendation/experts")
def recommend_experts(request: RecommendationRequest):
    return {"recommendations": result}
```

---

### 3. 관리자 매출 예측 AI

관리자 매출 예측 AI는 서비스 운영 데이터를 기반으로 예상 월 매출을 예측하는 기능입니다.

회원 수, 유료 구독자 수, 신규 가입자 수, 결제 성공률, 마케팅 비용 등의 데이터를 AI 서버로 전달합니다.  
AI는 이 데이터를 분석해 예상 월 매출을 반환하고, 관리자는 이를 운영 지표로 참고할 수 있습니다.

이 기능을 통해 관리자는 단순 통계 확인을 넘어 앞으로의 서비스 흐름을 예측할 수 있습니다.

**대표 코드**

```java
webClient.post()
    .uri("/regression/predict")
    .bodyValue(body);
```

```javascript
const prediction = await adminService.predictRevenue(payload);
renderRevenuePrediction(prediction);
```

```python
@app.post("/regression/predict")
def predict_revenue(request: RegressionRequest):
    return RegressionResponse(expectedMonthlyRevenue=prediction)
```

---

## 구현 포인트

- Spring Boot와 MyBatis를 사용해 견적 요청, 전문가 페이지, 관리자 페이지 API를 구현했습니다.
- JavaScript를 사용해 화면 데이터를 비동기로 조회하고, 목록과 차트를 동적으로 렌더링했습니다.
- FastAPI 기반 AI 서버를 Spring 서버와 연동해 견적 검토, 전문가 추천, 매출 예측 기능을 구현했습니다.
- Cloudflare Tunnel을 이용해 배포된 Spring 서버가 로컬 AI 서버와 통신할 수 있도록 연결했습니다.
- 발표용 더미데이터를 구성해 견적 요청, 전문가 활동, 관리자 통계 화면을 실제 서비스처럼 확인할 수 있도록 준비했습니다.
