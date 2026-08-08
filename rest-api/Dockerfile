# ---- Build ----
FROM golang:1.26 AS build
WORKDIR /src
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o /app .

# ---- RUN ----
FROM gcr.io/distroless/static-debian12
COPY --from=build /app /app
EXPOSE 8085
ENTRYPOINT ["/app"]
