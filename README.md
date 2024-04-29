# OpenTelemetry Tracing with Baggage Example

This is a simple Python script demonstrating how to use OpenTelemetry for distributed tracing with baggage propagation.

## Setup

1. Install OpenTelemetry Python package:

   ```bash
   pip install opentelemetry-api opentelemetry-sdk opentelemetry-exporter-otlp opentelemetry-baggage
   ```

2. Run the script:

   ```bash
   python main.py
   ```

## Explanation

- The `setup_tracing()` function sets up OpenTelemetry tracing with a BatchSpanProcessor and OTLP Span Exporter.
- The `main()` function demonstrates how to use OpenTelemetry for distributed tracing with baggage propagation.
- The script starts a main span and sets a correlation ID in the baggage. It then injects the baggage into headers using the W3C Baggage Propagator and the TraceContext Propagator.
- It extracts the context from headers and demonstrates how to retrieve baggage values.
- Two child spans are created with the extracted context, and the correlation ID is set in each span.

## Integrating Signoz

To visualize and analyze your traces, you can integrate Signoz. Signoz is an open-source monitoring and observability tool that provides end-to-end distributed tracing.

### Installation with Docker

You can install Signoz using Docker by following these steps:

1. Clone the Signoz repository:

   ```bash
   git clone https://github.com/SigNoz/signoz.git
   ```

2. Change directory to the Signoz repository:

   ```bash
   cd signoz
   ```

3. Run the Docker Compose command to start Signoz:

   ```bash
   docker-compose up -d
   ```

4. Access Signoz at [http://localhost:3000](http://localhost:3000) in your browser.

For more detailed installation instructions and configuration options, refer to the [Signoz documentation](https://signoz.io/docs/install/docker/).

## Dependencies

- [OpenTelemetry API](https://pypi.org/project/opentelemetry-api/): The OpenTelemetry API.
- [OpenTelemetry SDK](https://pypi.org/project/opentelemetry-sdk/): The OpenTelemetry SDK.
- [OpenTelemetry OTLP Exporter](https://pypi.org/project/opentelemetry-exporter-otlp/): OpenTelemetry exporter for OTLP.
- [OpenTelemetry Baggage](https://pypi.org/project/opentelemetry-baggage/): OpenTelemetry Baggage library.

## Contributing

Contributions are welcome! Please feel free to submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
