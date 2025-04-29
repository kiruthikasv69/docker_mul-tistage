1. Layer 1: Build stage setup (FROM ubuntu AS build)
FROM ubuntu AS build
This starts the first stage of the build using the Ubuntu base image.

2. Layer 2: Install dependencies (RUN apt-get update && apt-get install -y golang-go)
RUN apt-get update && apt-get install -y golang-go
This creates a layer that installs Golang inside the build stage.

3. Layer 3: Copy files into the image (COPY . .)
COPY . .
This layer copies the content of your local directory into the image.

4. Layer 4: Build the application (RUN CGO_ENABLED=0 go build -o /app .)
RUN CGO_ENABLED=0 go build -o /app .
This layer builds your Go application inside the container.

5. Layer 5: Scratch-based stage setup (FROM scratch)   
FROM scratch
This starts the second stage, where you use the empty scratch image to copy the compiled binary from the previous build stage.

6. Layer 6: Copy compiled binary (COPY --from=build /app /app)
COPY --from=build /app /app
This copies the /app binary built in the build stage to the scratch-based stage.

7. Layer 7: Set entrypoint (ENTRYPOINT ["/app"])
ENTRYPOINT ["/app"]
This sets the entrypoint for the container to the /app binary.
