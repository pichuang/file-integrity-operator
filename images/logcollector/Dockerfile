# Step one: build scapresults
FROM registry.access.redhat.com/ubi8/go-toolset as builder

WORKDIR /go/src/github.com/openshift/file-integrity-operator

ENV GOFLAGS=-mod=vendor
COPY . .
RUN make logcollector-bin

# Step two: containerize scapresults
FROM registry.access.redhat.com/ubi8/ubi

USER root

ENV LOGCOLLECTOR=/usr/local/bin/file-integrity-logcollector

# build scapresults
COPY --from=builder /go/src/github.com/openshift/file-integrity-operator/build/_output/bin/file-integrity-logcollector ${LOGCOLLECTOR}

ENTRYPOINT ["/usr/local/bin/file-integrity-logcollector"]
