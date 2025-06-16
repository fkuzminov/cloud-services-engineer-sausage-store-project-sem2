FROM golang:latest as build
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

FROM alpine:3.15
COPY --from=build /app/main .
RUN adduser -D -s /sbin/nologin nonroot && \
    chown nonroot:nonroot /app && chmod +x /app
USER nonroot
EXPOSE 8080
CMD ["/app/main"] 