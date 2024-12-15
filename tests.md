# TestMazzaTech

Goal: Achieve at least 80% test coverage for critical paths.
To our strategy, we have to create Unit Tests, focusing on individual components in isolation. The primary components to test include:
Input Validation: test the data (POST) endpoint for various valid and invalid payload (ex. Missing fields, incorrect data types)
Ensure the microservice returns the expected HTTP status codes and messages
Ensure the repository layer interacts with the database correctly
Business logic must be working perfectly.
Things related to security must be 100% tested and working very well. it's non-negotiable

Tools:
 * JUnit (Java)
 * Mockito for mocking dependencies
 * Testcontainers: Spins up real Docker containers for databases or other services during tests.
 * Spring Boot Test: To simulate HTTP requests and response

Small example
Test Data Persistence
@Test
void testSaveData() {
    DataEntity data = new DataEntity("example", "test");
    when(dataRepository.save(data)).thenReturn(data);

    DataEntity result = dataService.save(data);
    assertEquals(data.getName(), result.getName());
    verify(dataRepository, times(1)).save(data);
}

Scope:
Integration tests validate the interactions between multiple components or services, ensuring the system behaves correctly as a whole.

What to Test:
 * API Gateway:
 * Ensure it routes requests to the correct microservice.
 * Database Integration: Verify end-to-end data flow (e.g., saving and retrieving data).
 * Service Discovery: Confirm that the microservice can register with and query the Service Discovery component.

We want testing our performance with high level of requisitions. We have to ensure a high data of our clients making requests direct to our service. Our tests validate that the microservice meets the 500ms response time SLA under load.


Plan: Simulate millions of requests over time to evaluate:
 * API response time
 * Database query performance
 * Resource usage (CPU, memory)

Tools:
 * JMeter: For simulating high traffic to the endpoints.
 * Gatling: For load and stress testing.

Steps:
 * Create a load test script: 100 requests/second for 1 minute.
 * Scale up to 1,000 requests/second.
 * Measure response times and resource utilization.
 * Evaluate the performance degradation under load.

 <p>Future Testing Plans</p>

This is our future testing plan, trying to cover our entire application. We can implement a philosophy that every task must have a test to pass after that.
Test interdependencies between microservices once additional services are added to the architecture.
Performance Optimization (for identify specific points who we need to improve)
Introduce chaos testing to evaluate resilience during unexpected failures (e.g., network interruptions).
SQL injection.
Unauthorized access to endpoints.


