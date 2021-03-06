
![Overview](../../../media/quickstarts/overview-grpc.png)

This diagram shows how the signals flow in this quickstart. An [edge module](https://github.com/Azure/live-video-analytics/tree/master/utilities/rtspsim-live555) simulates an IP camera hosting a Real-Time Streaming Protocol (RTSP) server. An [RTSP source](../../../media-graph-concept.md#rtsp-source) node pulls the video feed from this server and sends video frames to the [motion detection processor](../../../media-graph-concept.md#motion-detection-processor) node. This processor will detect motion and upon detection will push video frames to the [gRPC extension processor](../../../media-graph-concept.md#grpc-extension-processor) node.

The gRPC extension node plays the role of a proxy. It converts the video frames to the specified image type. Then it relays the image over gRPC to another edge module that runs an AI model behind a gRPC endpoint over a [shared memory](https://en.wikipedia.org/wiki/Shared_memory). In this example, that edge module is built by using the [YOLOv3](https://github.com/Azure/live-video-analytics/tree/master/utilities/video-analysis/yolov3-onnx) model, which can detect many types of objects. The gRPC extension processor node gathers the detection results and publishes events to the [IoT Hub sink](https://docs.microsoft.com/azure/media-services/live-video-analytics-edge/media-graph-concept#iot-hub-message-sink) node. The node then sends those events to [IoT Edge Hub](https://docs.microsoft.com/azure/iot-edge/iot-edge-glossary#iot-edge-hub).

In this quickstart, you will:

1. Create and deploy the media graph.
1. Interpret the results.
1. Clean up resources.
