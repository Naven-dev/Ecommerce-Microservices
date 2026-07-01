# ============================================================
# Runtime — jar already built by GitHub Actions
# ============================================================
FROM eclipse-temurin:17-jre-alpine

RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

WORKDIR /app

COPY target/order-service-*.jar app.jar

ENV SPRING_H2_CONSOLE_ENABLED=false \
    SPRING_JPA_SHOW_SQL=false \
    SERVER_PORT=8082

EXPOSE 8082

HEALTHCHECK --interval=30s --timeout=5s --start-period=30s --retries=3 \
  CMD wget -qO- http://localhost:8082/actuator/health || exit 1

ENTRYPOINT ["java", \
  "-XX:+UseContainerSupport", \
  "-XX:MaxRAMPercentage=75.0", \
  "-Djava.security.egd=file:/dev/./urandom", \
  "-jar", "app.jar"]
