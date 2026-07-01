# ============================================================
# Runtime — jar already built by GitHub Actions
# ============================================================
FROM eclipse-temurin:17-jre-alpine

# Non-root user for security
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

WORKDIR /app

COPY target/product-service-*.jar app.jar

# Override dev-only properties at runtime via env vars
ENV SPRING_H2_CONSOLE_ENABLED=false \
    SPRING_JPA_SHOW_SQL=false \
    SERVER_PORT=8081

EXPOSE 8081

HEALTHCHECK --interval=30s --timeout=5s --start-period=30s --retries=3 \
  CMD wget -qO- http://localhost:8081/actuator/health || exit 1

ENTRYPOINT ["java", \
  "-XX:+UseContainerSupport", \
  "-XX:MaxRAMPercentage=75.0", \
  "-Djava.security.egd=file:/dev/./urandom", \
  "-jar", "app.jar"]
