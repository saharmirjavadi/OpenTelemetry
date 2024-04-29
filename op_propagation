from opentelemetry.trace.propagation.tracecontext import TraceContextTextMapPropagator
from opentelemetry.exporter.otlp.proto.grpc.trace_exporter import OTLPSpanExporter
from opentelemetry.baggage.propagation import W3CBaggagePropagator
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry import trace, baggage

def setup_tracing():
    """
    Sets up OpenTelemetry tracing with a BatchSpanProcessor and OTLP Span Exporter.
    """
    resource = trace.Resource(attributes={trace.SERVICE_NAME: "final"})
    provider = TracerProvider(resource=resource)
    processor = BatchSpanProcessor(OTLPSpanExporter(endpoint="http://127.0.0.1:4317"))
    provider.add_span_processor(processor)
    trace.set_tracer_provider(provider)
    return trace.get_tracer("my.tracer")

def main():
    """
    Main function to demonstrate OpenTelemetry tracing with baggage.
    """
    tracer = setup_tracing()

    with tracer.start_as_current_span("main") as span:
        ctx = baggage.set_baggage("correlation_id", "1")
        headers = {}
        W3CBaggagePropagator().inject(headers, ctx)
        TraceContextTextMapPropagator().inject(headers, ctx)
        print(f"Received headers: {headers}")

        carrier = {'traceparent': headers['traceparent']}
        ctx = TraceContextTextMapPropagator().extract(carrier=carrier)
        print(f"Received context: {ctx}")

        b2 = {'baggage': headers['baggage']}
        ctx2 = W3CBaggagePropagator().extract(b2, context=ctx)
        print(f"Received context2: {ctx2}")

        with tracer.start_span("child_1", context=ctx2) as span:
            span.set_attribute('correlation_id', 123)
            print(baggage.get_baggage('correlation_id', ctx2))

        with tracer.start_span("child_2", context=ctx2) as span2:
            span2.set_attribute('correlation_id', 123)
            print(baggage.get_baggage('correlation_id', ctx2)))

if __name__ == "__main__":
    main()
