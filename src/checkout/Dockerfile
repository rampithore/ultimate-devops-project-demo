FROM golang:1.22-alpine AS builder

WORKDIR /usr/src/app/

# Cache modules
COPY go.mod go.sum ./
RUN go mod download

# Copy source
COPY . .

# Build binary (output path: /go/bin/checkout
RUN go build -o /go/bin/checkout ./

# ---------- Run stage ----------
FROM alpine
WORKDIR /usr/src/app/
# If your app makes HTTPS calls, copy certificates

# ✅ Copy the built binary from correct location
COPY --from=builder /go/bin/checkout ./
EXPOSE ${CHECKOUT_PORT}
ENV CHECKOUT_PORT 80000
# Run the binary
ENTRYPOINT ["./checkout"]
