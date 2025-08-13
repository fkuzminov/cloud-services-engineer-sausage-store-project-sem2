FROM golang:latest AS build
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

FROM alpine:3.15
WORKDIR /app
COPY --from=build /app/main .
EXPOSE 8080
CMD ["/app/main"]
