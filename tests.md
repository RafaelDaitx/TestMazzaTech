# Testing

Our goal is to achieve at least 80% test coverage for critical paths.

To our strategy, we have to create Unit Tests, focusing on individual components in isolation. The primary components to test include:<br>
<b>Input Validation:</b> test the data (POST) endpoint for various valid and invalid payload (ex. Missing fields, incorrect data types)<br>
<b>Ensure the microservice returns the expected HTTP status codes and messages</b><br>
<b>Ensure the repository layer interacts with the database correctly</b><br>
<b>Business logic must be working perfectly.</b><br>
Things related to security must be <b>100%</b> tested and working very well. it's non-negotiable<br>

Tools:
 * JUnit (Java)<br>
 * Mockito for mocking dependencies<br>
 * Testcontainers: Spins up real Docker containers for databases or other services during tests.<br>
 * Spring Boot Test: To simulate HTTP requests and response<br>

Small example<br>
Test Data Persistence<br>

```yaml
@Test
void testSaveData() {
    DataEntity data = new DataEntity("example", "test");
    when(dataRepository.save(data)).thenReturn(data);

    DataEntity result = dataService.save(data);
    assertEquals(data.getName(), result.getName());
    verify(dataRepository, times(1)).save(data);
}
```
<br>
Scope:
Integration tests validate the interactions between multiple components or services, ensuring the system behaves correctly as a whole.
<br>
What to Test:
 * API Gateway:<br>
 * Ensure it routes requests to the correct microservice.<br>
 * Database Integration: Verify end-to-end data flow (e.g., saving and retrieving data).<br>
 * Service Discovery: Confirm that the microservice can register with and query the Service Discovery component.<br>

We want testing our performance with high level of requisitions. We have to ensure a high data of our clients <br>making requests direct to our service. Our tests validate that the microservice meets the 500ms response time SLA under load.<br>


Plan: Simulate millions of requests over time to evaluate:<br>
 * API response time<br>
 * Database query performance<br>
 * Resource usage (CPU, memory)<br>

Tools:<br>
 * JMeter: For simulating high traffic to the endpoints.<br>
 * Gatling: For load and stress testing.<br>

Steps:<br>
 * Create a load test script: 100 requests/second for 1 minute.<br>
 * Scale up to 1,000 requests/second.<br>
 * Measure response times and resource utilization.<br>
 * Evaluate the performance degradation under load.<br>
<br><br>
 
 <p>Future Testing Plans</p><br>

This is our future testing plan, trying to cover our entire application. We can implement a philosophy that every task must have a test to pass after that.<br>
Test interdependencies between microservices once additional services are added to the architecture.<br>
Performance Optimization (for identify specific points who we need to improve)<br>
Introduce chaos testing to evaluate resilience during unexpected failures (e.g., network interruptions).
SQL injection.<br>
Unauthorized access to endpoints.<br>


