# Build stage
FROM golang:1.21 AS base

WORKDIR /app

# Copy go.mod and go.sum files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy application source code
COPY . .

# Build the Go application
RUN go build -o main .

# Final stage - Distroless image
FROM gcr.io/distroless/base

WORKDIR /app

# Copy binary from build stage
COPY --from=base /app/main .

# Copy static files
COPY --from=base /app/static ./static

EXPOSE 8080

CMD ["./main"]