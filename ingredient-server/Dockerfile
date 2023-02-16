##Build
FROM golang:buster AS build

WORKDIR /app

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY *.go ./

RUN go build -o /ingredient-server

## Deploy
FROM gcr.io/distroless/base-debian10

WORKDIR /

COPY --from=build /ingredient-server /ingredient-server

EXPOSE 30123

USER nonroot:nonroot

ENTRYPOINT ["/ingredient-server"]