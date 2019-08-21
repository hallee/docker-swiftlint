FROM swift:5.0.1-bionic as builder
# SwiftLint currently fails to build on Swift 5.1 on Linux

ENV SWIFTLINT_REVISION="master"

# Install SwiftLint
RUN git clone --branch $SWIFTLINT_REVISION https://github.com/realm/SwiftLint.git && \
    cd SwiftLint && \
    git submodule update --init --recursive; make install && \
    mv `swift build --configuration release --static-swift-stdlib --show-bin-path`/swiftlint /usr/bin

FROM vapor/swift:5.1-bionic
COPY --from=builder /usr/bin/swiftlint /bin/
RUN swiftlint version
CMD ["swiftlint", "lint"]
