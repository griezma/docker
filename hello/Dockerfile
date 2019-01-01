FROM alpine as build
COPY hello.c .
RUN apk --no-cache add g++
RUN gcc -o hello -static -nostartfiles hello.c

FROM scratch
COPY --from=build /hello /
CMD ["/hello"]