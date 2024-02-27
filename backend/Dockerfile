# Install official image golang 
FROM golang:1.22-alpine3.18 as build
# Add a work directory
WORKDIR /app
# Cache and install dependencies
COPY go.mod go.sum ./
RUN go mod download
# Copy app files
COPY . .
# compile application
RUN go build -o api /app/cmd/api
##
## STEP 2 - DEPLOY
##
FROM alpine:3.18
# Add a work directory
WORKDIR /
# Copy built binary from builder
COPY --from=build /app/api /backend
# Expose port
EXPOSE 8081
# Start app
ENTRYPOINT ["/backend"]