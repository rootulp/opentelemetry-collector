# Changelog

## Unreleased

### 🛑 Breaking changes 🛑

- Remove deprecated funcs/types from service related to `Config` (#5755)
- Change`confighttp.ToClient` to accept a `component.Host` (#5737)
- Remove deprecated funcs from pdata related to mutable slices (#5754)
- Change the following deprecated component functions to ensure a stability level is set:
  - `component.WithTracesExporter`
  - `component.WithMetricsExporter`
  - `component.WithLogsExporter`
  - `component.WithTracesReceiver`
  - `component.WithMetricsReceiver`
  - `component.WithLogsReceiver`
  - `component.WithTracesProcessor`
  - `component.WithMetricsProcessor`
  - `component.WithLogsProcessor`

### 🚩 Deprecations 🚩

- Deprecate the following component functions added to ensure a stability level is set:
  - `component.WithTracesExporterAndStabilityLevel` -> `component.WithTracesExporter`
  - `component.WithMetricsExporterAndStabilityLevel` -> `component.WithMetricsExporter`
  - `component.WithLogsExporterAndStabilityLevel` -> `component.WithLogsExporter`
  - `component.WithTracesReceiverAndStabilityLevel` -> `component.WithTracesReceiver`
  - `component.WithMetricsReceiverAndStabilityLevel` -> `component.WithMetricsReceiver`
  - `component.WithLogsReceiverAndStabilityLevel` -> `component.WithLogsReceiver`
  - `component.WithTracesProcessorAndStabilityLevel` -> `component.WithTracesProcessor`
  - `component.WithMetricsProcessorAndStabilityLevel` -> `component.WithMetricsProcessor`
  - `component.WithLogsProcessorAndStabilityLevel` -> `component.WithLogsProcessor`
  - 
### 💡 Enhancements 💡

- `ocb` now exits with an error if it fails to load the build configuration. (#5731)
- Deprecate `HTTPClientSettings.ToClientWithHost` (#5737)

### 🧰 Bug fixes 🧰

- Fix bug in ocb where flags did not take precedence. (#5726)

## v0.56.0 Beta

### 💡 Enhancements 💡

- Add `linux-ppc64le` architecture to cross build tests in CI (#5645)
- `client`: perform case insensitive lookups in case the requested metadata value isn't found (#5646)
- `loggingexporter`: Decouple `loglevel` field from level of logged messages (#5678)
- Expose `pcommon.NewSliceFromRaw` function (#5679)
- `loggingexporter`: create the exporter's logger from the service's logger (#5677)
- Add `otelcol_exporter_queue_capacity` metrics show the collector's exporter queue capacity (#5475)
- Add support to handle 402, 413, 414, 431 http error code as permanent errors in OTLP exporter (#5685)

### 🧰 Bug fixes 🧰

- Fix Collector panic when disabling telemetry metrics (#5642)
- Fix Collector panic when featuregate value is empty (#5663)
- Fix confighttp.compression panic due to nil request.Body. (#5628)

## v0.55.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated `config.ServiceTelemetry` (#5565)
- Remove deprecated `config.ServiceTelemetryLogs` (#5565)
- Remove deprecated `config.ServiceTelemetryMetrics` (#5565)

### 🚩 Deprecations 🚩

- Deprecate `service.ConfigServiceTelemetry`, `service.ConfigServiceTelemetryLogs`, and `service.ConfigServiceTelemetryMetrics` (#5565)
- Deprecate the following component functions to ensure a stability level is set (#5580):
  - `component.WithTracesExporter` -> `component.WithTracesExporterAndStabilityLevel`
  - `component.WithMetricsExporter` -> `component.WithMetricsExporterAndStabilityLevel`
  - `component.WithLogsExporter` -> `component.WithLogsExporterAndStabilityLevel`
  - `component.WithTracesReceiver` -> `component.WithTracesReceiverAndStabilityLevel`
  - `component.WithMetricsReceiver` -> `component.WithMetricsReceiverAndStabilityLevel`
  - `component.WithLogsReceiver` -> `component.WithLogsReceiverAndStabilityLevel`
  - `component.WithTracesProcessor` -> `component.WithTracesProcessorAndStabilityLevel`
  - `component.WithMetricsProcessor` -> `component.WithMetricsProcessorAndStabilityLevel`
  - `component.WithLogsProcessor` -> `component.WithLogsProcessorAndStabilityLevel`
- Deprecate `Registry.Apply` in `service.featuregate` (#5660)

### 💡 Enhancements 💡

- Components stability levels are now logged. By default components which haven't defined their stability levels, or which are
  unmaintained, deprecated or in development will log a message. (#5580)
- `exporter/logging`: Skip "bad file descriptor" sync errors (#5585)

### 🧰 Bug fixes 🧰

- Fix initialization of the OpenTelemetry MetricProvider. (#5571)
- Set log level for `undefined` stability level to debug. (#5635)

## v0.54.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated `GetLogger`. (#5504)
- Remove deprecated `configtest.LoadConfigMap` (#5505)
- Remove deprecated `config.Map` (#5505)
- Remove deprecated `config.MapProvider` (#5505)
- Remove deprecated `config.MapConverter` (#5505)
- Remove deprecated `config.Received` (#5505)
- Remove deprecated `config.CloseFunc` (#5505)
- Deprecated `pcommon.Value.NewValueBytes` is brought back taking `pcommon.ImmutableByteSlice` as an argument instead of `[]byte` (#5299)

### 🚩 Deprecations 🚩

- Use immutable slices for primitive types slices to restrict mutations. (#5299)
  - `Value.NewValueMBytes` func is deprecated in favor of `Value.NewValueBytes` func that takes
    `ImmutableByteSlice` instead of `[]byte`
  - `Value.SetMBytesVal` func is deprecated in favor of `Value.SetBytesVal` func that takes
    `pcommon.ImmutableByteSlice` instead of []byte.
  - `Value.BytesVal` func is deprecated in favor of `Value.BytesVal` func that returns `pcommon.ImmutableByteSlice`
    instead of []byte.
  - `<HistogramDataPoint|Buckets>.SetMBucketCounts` funcs are deprecated in favor of
    `<HistogramDataPoint|Buckets>.SetBucketCounts` funcs that take `pcommon.ImmutableUInt64Slice` instead of []uint64.
  - `<HistogramDataPoint|Buckets>.MBucketCounts` funcs are deprecated in favor of
    `<HistogramDataPoint|Buckets>.BucketCounts` funcs that return `pcommon.ImmutableUInt64Slice` instead of []uint64.
  - `HistogramDataPoint.SetMExplicitBounds` func is deprecated in favor of `HistogramDataPoint.SetExplicitBounds` func
    that takes `pcommon.ImmutableFloat64Slice` instead of []float64.
  - `HistogramDataPoint.MExplicitBounds` func func is deprecated in favor of `HistogramDataPoint.ExplicitBounds`
    returns `pcommon.ImmutableFloat64Slice` instead of []float64.

### 💡 Enhancements 💡

- Deprecate `HTTPClientSettings.ToClient` in favor of `HTTPClientSettings.ToClientWithHost` (#5584)
- Use OpenCensus `metric` package for process metrics instead of `stats` package (#5486)
- Update OTLP to v0.18.0 (#5530)
- Log histogram min/max fields with `logging` exporter (#5520)

### 🧰 Bug fixes 🧰

- Update sum field of exponential histograms to make it optional (#5530)
- Remove redundant extension shutdown call (#5532)
- Refactor pipelines builder, fix some issues (#5512)
  - Unconfigured receivers are not identified, this was not a real problem in final binaries since the validation of the config catch this.
  - Allow configurations to contain "unused" receivers. Receivers that are configured but not used in any pipeline, this was possible already for exporters and processors.
  - Remove the enforcement/check that Receiver factories create the same instance for the same config.

## v0.53.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated `componenterror` package. (#5420)
- Remove deprecated `config.MapConverterFunc`. (#5419)
- Remove `AddCollectorVersionTag`, enabled for long time already. (#5471)

### 🚩 Deprecations 🚩

- Move `config.Map` to its own package `confmap` which does not depend on any component concept (#5237)
  - `config.Map` -> `confmap.ConfMap`
  - `config.MapProvider` -> `confmap.Provider`
  - `config.Received` -> `confmap.Received`
  - `config.NewReceivedFromMap` -> `confmap.NewReceived`
  - `config.CloseFunc` -> `confmap.CloseFunc`
  - `config.ChangeEvent` -> `confmap.ChangeEvent`
  - `config.MapConverter` -> `confmap.Converter`
  - Package `envmapprovider` -> `envprovider`
  - Package `filemapprovider` -> `fileprovider`
  - Package `yamlmapprovider` -> `yamlprovider`
  - Package `expandmapconverter` -> `expandconverter`
  - Package `filemapprovider` -> `fileprovider`
  - Package `overwritepropertiesmapconverter` -> `overwritepropertiesconverter`
- Deprecate `component.ExtensionDefaultConfigFunc` in favor of `component.ExtensionCreateDefaultConfigFunc` (#5451)
- Deprecate `confmap.Received.AsMap` in favor of `confmap.Received.AsConf` (#5465)
- Deprecate `confmap.Conf.Set`, not used anywhere for the moment (#5485)

### 💡 Enhancements 💡

- Move `service.mapResolver` to `confmap.Resolver` (#5444)
- Add `linux-arm` architecture to cross build tests in CI (#5472)

### 🧰 Bug fixes 🧰

- Fixes the "service.version" label value for internal metrics, always was "latest" in core/contrib distros. (#5449).
- Send correct batch stats when SendBatchMaxSize is set (#5385)
- TLS `MinVersion` and `MaxVersion` defaults will be handled by `crypto/tls` (#5480)

## v0.52.0 Beta

### 🛑 Breaking changes 🛑

- Remove `configunmarshaler.Unmarshaler` interface, per deprecation comment (#5348)
- Remove deprecated pdata funcs/structs from v0.50.0 (#5345)
- Remove deprecated pdata getters and setters of primitive slice values: `Value.BytesVal`, `Value.SetBytesVal`, 
  `Value.UpdateBytes`, `Value.InsertBytes`, `Value.UpsertBytes`, `<HistogramDataPoint|Buckets>.BucketCounts`, 
  `<HistogramDataPoint|Buckets>.SetBucketCounts`, `HistogramDataPoint.ExplicitBounds`,
  `HistogramDataPoint.SetExplicitBounds` (#5347)
- Remove deprecated featuregate funcs/structs from v0.50.0 (#5346)
- Remove access to deprecated members of the config.Retrieved struct (#5363)
- Replace usage of `config.MapConverterFunc` with `config.MapConverter` (#5382)

### 🚩 Deprecations 🚩

- Deprecate `config.Config` and `config.Service`, use `service.Config*` (#4608)
- Deprecate `componenterror` package, move everything to `component` (#5383)
- `pcommon.Value.NewValueBytes` is deprecated in favor of `Value.NewValueMBytes` in preparation of migration to 
  immutable slices (#5367)

### 💡 Enhancements 💡

- Update OTLP to v0.17.0 (#5335)
- Add optional min/max fields to histograms (#5399)
- User-defined Resource attributes can be specified under `service.telemetry.resource`
  configuration key and will be included as metric lables for own telemetry.
  If `service.instance.id` is not specified it will be auto-generated. Previously
  `service.instance.id` was always auto-generated, so the default of the new
  behavior matches the old behavior. (#5402)

## v0.51.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated model module, everything is available in `pdata` and `semconv`. (#5281)
  - Old versions of the module are still available, but no new versions will be released.
- Remove deprecated LogRecord.Name field. (#5202)

### 🚩 Deprecations 🚩

- In preparation of migration to immutable slices for primitive type items, the following methods are renamed (#5344)
  - `Value.BytesVal` func is deprecated in favor of `Value.MBytesVal`.
  - `Value.SetBytesVal` func is deprecated in favor of `Value.SetMBytesVal`.
  - `Value.UpdateBytes` func is deprecated in favor of `Value.UpdateMBytes`.
  - `Value.InsertBytes` func is deprecated in favor of `Value.InsertMBytes`.
  - `Value.UpsertBytes` func is deprecated in favor of `Value.UpsertMBytes`.
  - `<HistogramDataPoint|Buckets>.BucketCounts` funcs are deprecated in favor of
    `<HistogramDataPoint|Buckets>.MBucketCounts`.
  - `<HistogramDataPoint|Buckets>.SetBucketCounts` funcs are deprecated in favor of
    `<HistogramDataPoint|Buckets>.SetMBucketCounts`.
  - `HistogramDataPoint.ExplicitBounds` func is deprecated in favor of `HistogramDataPoint.MExplicitBounds`.
  - `HistogramDataPoint.SetExplicitBounds` func is deprecated in favor of `HistogramDataPoint.SetMExplicitBounds`.

### 💡 Enhancements 💡

- `pdata`: Expose `pcommon.NewSliceFromRaw` and `pcommon.Slice.AsRaw` functions (#5311)

### 🧰 Bug fixes 🧰

- Fix Windows Event Logs ignoring user-specified logging options (#5298)

## v0.50.0 Beta

### 🛑 Breaking changes 🛑

- Remove pdata deprecated funcs from 2 versions (v0.48.0) ago. (#5219)
- Remove non pdata deprecated funcs/structs (#5220)
- `pmetric.Exemplar.ValueType()` now returns new type `ExemplarValueType` (#5233)
- Remove deprecated `Delete` pdata func in favor of `pdata.Remove` from (v0.47.0). (#5307)

### 🚩 Deprecations 🚩

- Deprecate `configunmarshaler` package, move it to internal (#5151)
- Deprecate all API in `model/semconv`. The package is moved to a new `semcomv` module (#5196)
- Deprecate access to `config.Retrieved` fields, use the newly added funcs to interact with the internal fields (#5198)
- Deprecate `p<signal>otlp.Request.Set<Logs|Metrics|Traces>` (#5234)
  - `plogotlp.Request.SetLogs` func is deprecated in favor of `plogotlp.NewRequestFromLogs`
  - `pmetricotlp.Request.SetMetrics` func is deprecated in favor of `pmetricotlp.NewRequestFromMetrics`
  - `ptraceotlp.Request.SetTraces` func is deprecated in favor of `ptraceotlp.NewRequestFromTraces`
- `pmetric.NumberDataPoint.ValueType()` now returns new type `NumberDataPointValueType` (#5233)
  - `pmetric.MetricValueType` is deprecated in favor of `NumberDataPointValueType`
  - `pmetric.MetricValueTypeNone` is deprecated in favor of `NumberDataPointValueTypeNone`
  - `pmetric.MetricValueTypeInt` is deprecated in favor of `NumberDataPointValueTypeInt`
  - `pmetric.MetricValueTypeDouble` is deprecated in favor of `NumberDataPointValueTypeDouble`
- Deprecate `plog.LogRecord.SetName()` function (#5230)
- Deprecate global `featuregate` funcs in favor of `GetRegistry` and a public `Registry` type (#5160)

### 💡 Enhancements 💡
- Add `jsoniter` Unmarshaller (#4817)

- Extend config.Map.Unmarshal hook to check map key string to any TextUnmarshaler not only ComponentID (#5244)
- Collector will no longer print error with stack trace when the collector is shutdown due to a context cancel. (#5258)

### 🧰 Bug fixes 🧰
- Fix translation from otlp.Request to pdata representation, changes to the returned pdata not all reflected to the otlp.Request (#5197)
- `exporterhelper` now properly consumes any remaining items on stop (#5203)
- `pdata`: Fix copying of `Value` with `ValueTypeBytes` type (#5267)
- `pdata`: Fix copying of metric fields of primitive items slice type (#5271)

## v0.49.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated structs/funcs from previous versions (#5131)
- Do not set TraceProvider to global otel (#5138)
- Remove deprecated funcs from otlpgrpc (#5144)
- Add Scheme to MapProvider interface (#5068)
- Do not set MeterProvider to global otel (#5146)
- Make `InstrumentationLibrary<signal>ToScope` helper functions unexported (#5164)
- Remove Log's "ShortName" from logging exporter output (#5172)
- `exporter/otlp`: Retry RESOURCE_EXHAUSTED only if the server returns RetryInfo (#5147)

### 🚩 Deprecations 🚩

- All pdata related APIs from model (model/pdata, model/otlp and model/otlpgrpc) are deprecated in
  favor of packages in the new pdata module separated by telemetry signal type (#5168)
  - `model/pdata`, `model/otlp` -> `pdata/pcommon`, `pdata/plog`, `pdata/pmetric`, `pdata/ptrace`
  - `model/otlpgrpc` -> `pdata/plog/plogotlp`, `pdata/pmetric/pmetricotlp`, `pdata/ptrace/ptraceotlp`
- Deprecate configmapprovider package, replace with mapconverter (#5167)
- Deprecate `service.MustNewConfigProvider` and `service.MustNewDefaultConfigProvider`in favor of `service.NewConfigProvider` (#4936)

### 💡 Enhancements 💡

- OTLP HTTP receiver will use HTTP/2 over TLS if client supports it (#5109) 
- Add `ObservedTimestamp` field to `pdata.LogRecord` (#5171)

### 🧰 Bug fixes 🧰

- Setup the correct meter provider if telemetry.useOtelForInternalMetrics featuregate enabled (#5146)
- Fix pdata.Value.asRaw() to correctly return elements of Slice and Map type (#5153)
- Update pdata.Slice.asRaw() to return raw representation of Slice and Map elements (#5157)
- The codepath through the OTLP receiver for gRPC was not translating the InstrumentationLibrary* to Scope* (#5189)

## v0.48.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated `consumerhelper` package (#5028)
- Remove pdata `InternalRep` deprecated funcs (#5018)
- Remove service/defaultcomponents deprecated package (#5019)
- Remove deprecated UseOpenTelemetryForInternalMetrics (#5026)
- Change outcome of `pdata.Value.MapVal()` and `pdata.Value.SliceVal()` functions misuse. In case of
  type mismatch, they now return an invalid zero-initialized instance instead of a detached
  collection (#5034)
- OTLP JSON field changes following upgrade to OTLP v0.15.0:
  - "instrumentationLibraryLogs" is now "scopeLogs"
  - "instrumentationLibraryMetrics" is now "scopeMetrics"
  - "instrumentationLibrarySpans" is now "scopeSpans"
  - "instrumentationLibrary" is now "scope"
- AsString for pdata.Value now returns the JSON-encoded string of floats. (#4934)

### 🚩 Deprecations 🚩

- Move MapProvider to config, split providers in their own package (#5030)
- API related to `pdata.AttributeValue` is deprecated in favor of `pdata.Value` (#4978)
  - `pdata.AttributeValue` struct is deprecated in favor of `pdata.Value`
  - `pdata.AttributeValueType` type is deprecated in favor of `pdata.ValueType`
  - `pdata.AttributeValueType...` constants are deprecated in favor of `pdata.ValueType...`
  - `pdata.NewAttributeValue...` funcs are deprecated in favor of `pdata.NewValue...`
- Deprecate featureflags.FlagValue.SetSlice, unnecessary public (#5053)
- Remove "Attribute" part from common pdata collections names (#5001)
  - Deprecate `pdata.AttributeMap` struct in favor of `pdata.Map`
  - Deprecate `pdata.NewAttributeMap` func in favor of `pdata.NewMap`
  - Deprecate `pdata.NewAttributeMapFromMap` func in favor of `pdata.NewMapFromRaw`
  - Deprecate `pdata.AttributeValueSlice` struct in favor of `pdata.Slice`
  - Deprecate `pdata.NewAttributeValueSlice` func in favor of `pdata.NewSlice`
- Deprecate LogRecord.Name(), it was deprecated in the data model (#5054)
- Rename `Array` type of `pdata.Value` to `Slice` (#5066)
  - Deprecate `pdata.AttributeValueTypeArray` type in favor of `pdata.ValueTypeSlice`
  - Deprecate `pdata.NewAttributeValueArray` func in favor of `pdata.NewValueSlice`
- Deprecate global flag in `featuregates` (#5060)
- Deprecate last funcs/structs in componenthelper (#5069)
- Change structs in otlpgrpc to follow standard go encoding interfaces (#5062)
  - Deprecate UnmarshalJSON[Traces|Metrics|Logs][Reques|Response] in favor of `UnmarshalJSON`.
  - Deprecate [Traces|Metrics|Logs][Reques|Response].Marshal in favor of `MarshalProto`.
  - Deprecate UnmarshalJSON[Traces|Metrics|Logs][Reques|Response] in favor of `UnmarshalProto`.
- Deprecating following pdata methods/types following OTLP v0.15.0 upgrade (#5076):
      - InstrumentationLibrary is now InstrumentationScope
      - NewInstrumentationLibrary is now NewInstrumentationScope
      - InstrumentationLibraryLogsSlice is now ScopeLogsSlice
      - NewInstrumentationLibraryLogsSlice is now NewScopeLogsSlice
      - InstrumentationLibraryLogs is now ScopeLogs
      - NewInstrumentationLibraryLogs is now NewScopeLogs
      - InstrumentationLibraryMetricsSlice is now ScopeMetricsSlice
      - NewInstrumentationLibraryMetricsSlice is now NewScopeMetricsSlice
      - InstrumentationLibraryMetrics is now ScopeMetrics
      - NewInstrumentationLibraryMetrics is now NewScopeMetrics
      - InstrumentationLibrarySpansSlice is now ScopeSpansSlice
      - NewInstrumentationLibrarySpansSlice is now NewScopeSpansSlice
      - InstrumentationLibrarySpans is now ScopeSpans
      - NewInstrumentationLibrarySpans is now NewScopeSpans
      
### 💡 Enhancements 💡

- Add semconv definitions for v1.9.0 (#5090)
- Change outcome of `pdata.Metric.<Gauge|Sum|Histogram|ExponentialHistogram>()` functions misuse.
  In case of type mismatch, they don't panic right away but return an invalid zero-initialized
  instance for consistency with other OneOf field accessors (#5035)
- Update OTLP to v0.15.0 (#5064)
- Adding support for transition from older versions of OTLP to OTLP v0.15.0 (#5085)

### 🧰 Bug fixes 🧰

- Add missing files for semconv definitions v1.7.0 and v1.8.0 (#5091)
- The `featuregates` were not configured from the "--feature-gates" flag on windows service (#5060)
- Fix Semantic Convention Schema URL definition for 1.5.0 and 1.6.1 versions (#5103)

## v0.47.0 Beta

### 🛑 Breaking changes 🛑

- Remove `Type` funcs in pdata (#4933)
- Remove all deprecated funcs/structs from v0.46.0 (#4995)

### 🚩 Deprecations 🚩

- pdata: deprecate funcs working with InternalRep (#4957)
- Deprecate `pdata.AttributeMap.Delete` in favor of `pdata.AttributeMap.Remove` (#4914)
- Deprecate consumerhelper, move helpers to consumer (#5006)

### 💡 Enhancements 💡

- Add `pdata.AttributeMap.RemoveIf`, which is a more performant way to remove multiple keys (#4914)
- Add `pipeline` key with pipeline identifier to processor loggers (#4968)
- Add a new yaml provider, allows providing yaml bytes (#4998)

### 🧰 Bug fixes 🧰

- Collector `Run` will now exit when a context cancels (#4954)
- Add missing droppedAttributesCount to pdata generated resource (#4979)
- Collector `Run` will now set state to `Closed` if startup fails (#4974)

## v0.46.0 Beta

### 🛑 Breaking changes 🛑

- Change otel collector to enable open telemetry metrics through feature gate instead of a constant (#4912)
- Remove support for legacy otlp/http port. (#4916)
- Remove deprecated funcs in pdata (#4809)
- Remove deprecated Retrieve funcs/calls (#4922)
- Remove deprecated NewConfigProvider funcs (#4937)

### 🚩 Deprecations 🚩

- Deprecated funcs `config.DefaultConfig`, `confighttp.DefaultHTTPSettings`, `exporterhelper.DefaultTimeoutSettings`, 
  `exporthelper.DefaultQueueSettings`, `exporterhelper.DefaultRetrySettings`, `testcomponents.DefaultFactories`, and
  `scraperhelper.DefaultScraperControllerSettings` in favour for their `NewDefault` method to adhere to contribution guidelines (#4865)
- Deprecated funcs `componenthelper.StartFunc`, `componenthelper.ShutdownFunc` in favour of `component.StartFunc` and `component.ShutdownFunc` (#4803)
- Move helpers from extensionhelper to component (#4805)
  - Deprecated `extensionhelper.CreateDefaultConfig` in favour of `component.ExtensionDefaultConfigFunc`
  - Deprecated `extensionhelper.CreateServiceExtension` in favour of `component.CreateExtensionFunc`
  - Deprecated `extensionhelper.NewFactory` in favour of `component.NewExtensionFactory`
- Move helpers from processorhelper to component (#4889)
  - Deprecated `processorhelper.CreateDefaultConfig` in favour of `component.ProcessorDefaultConfigFunc`
  - Deprecated `processorhelper.WithTraces` in favour of `component.WithTracesProcessor`
  - Deprecated `processorhelper.WithMetrics` in favour of `component.WithMetricsProcessor`
  - Deprecated `processorhelper.WithLogs` in favour of `component.WithLogsProcessor`
  - Deprecated `processorhelper.NewFactory` in favour of `component.NewProcessorFactory`
- Move helpers from exporterhelper to component (#4899)
  - Deprecated `exporterhelper.CreateDefaultConfig` in favour of `component.ExporterDefaultConfigFunc`
  - Deprecated `exporterhelper.WithTraces` in favour of `component.WithTracesExporter`
  - Deprecated `exporterhelper.WithMetrics` in favour of `component.WithMetricsExporter`
  - Deprecated `exporterhelper.WithLogs` in favour of `component.WithLogsExporter`
  - Deprecated `exporterhelper.NewFactory` in favour of `component.NewExporterFactory`
- Move helpers from receiverhelper to component (#4891)
  - Deprecated `receiverhelper.CreateDefaultConfig` in favour of `component.ReceiverDefaultConfigFunc`
  - Deprecated `receiverhelper.WithTraces` in favour of `component.WithTracesReceiver`
  - Deprecated `receiverhelper.WithMetrics` in favour of `component.WithMetricsReceiver`
  - Deprecated `receiverhelper.WithLogs` in favour of `component.WithLogsReceiver`
  - Deprecated `receiverhelper.NewFactory` in favour of `component.NewReceiverFactory`

### 💡 Enhancements 💡

- Add validation to check at least one endpoint is specified in otlphttpexporter's configuration (#4860)
- Implement default client authenticators (#4837)

## 🧰 Bug fixes 🧰

- Initialized logger with collector to avoid potential race condition panic on `Shutdown` (#4827)
- In addition to traces, now logs and metrics processors will start the memory limiter.
  Added thread-safe logic so only the first processor can launch the `checkMemLimits` go-routine and the last processor
  that calls shutdown to terminate it; this is done per memory limiter instance.
  Added memory limiter factory to cache initiated object and be reused by similar config. This guarantees a single
  running `checkMemLimits` per config (#4886)
- Resolved race condition in collector when calling `Shutdown` (#4878)

## v0.45.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated funcs in configtelemetry (#4808)
- `otlphttp` and `otlp` exporters enable gzip compression by default (#4632)

### 🚩 Deprecations 🚩

- Deprecate `service/defaultcomponents` go package (#4622)
- Deprecate `pdata.NumberDataPoint.Type()` and `pdata.Exemplar.Type()` in favor of `NumberDataPoint.ValueType()` and
  `Exemplar.ValueType()` (#4850)

### 💡 Enhancements 💡

- Reject invalid queue size exporterhelper (#4799)
- Transform configmapprovider.Retrieved interface to a struct (#4789)
- Added feature gate summary to zpages extension (#4834)
- Add support for reloading TLS certificates (#4737)

### 🧰 Bug fixes 🧰

- `confighttp`: Allow CORS requests with configured auth (#4869)

## v0.44.0 Beta

### 🛑 Breaking changes 🛑

- Updated to OTLP 0.12.0. Deprecated traces and metrics messages that existed
  in 0.11.0 are no longer converted to the messages and fields that replaced the deprecated ones.
  Received deprecated messages and fields will be now ignored. In OTLP/JSON in the
  instrumentationLibraryLogs object the "logs" field is now named "logRecords" (#4724)
- Deprecate `service.NewWindowsService`, add `service.NewSvcHandler` (#4783).

### 🚩 Deprecations 🚩

- Deprecate `service.NewConfigProvider`, and a new version `service.MustNewConfigProvider` (#4734).

### 💡 Enhancements 💡

- Invalid requests now return an appropriate unsupported (`405`) or method not allowed (`415`) response (#4735)
- `client.Info`: Add Host property for Metadata (#4736)

## v0.43.1 Beta

### 🧰 Bug fixes 🧰

- ExpandStringValues function support to map[string]interface{} (#4748) 

## v0.43.0 Beta

### 🛑 Breaking changes 🛑

- Change configmapprovider.Provider to accept a location for retrieve (#4657)
- Change Properties Provider to be a Converter (#4666)
- Define a type `WatcherFunc` for onChange func instead of func pointer (#4656)
- Remove deprecated `configtest.LoadConfig` and `configtest.LoadConfigAndValidate` (#4659)
- Move service.ConfigMapConverterFunc to config.MapConverterFunc (#4673)
  - Add context to config.MapConverterFunc (#4678)
- Builder: the skip compilation should only be supplied as a CLI flag. Previously, it was possible to specify that in the YAML file, contrary to the original intention (#4645)
- Builder: Remove deprecated config option module::core (#4693)
- Remove deprecate flags --metrics-level and --metrics-addr (#4695)
  - Usages of `--metrics-level={VALUE}` can be replaced by `--set=service.telemetry.metrics.level={VALUE}`;
  - Usages of `--metrics-addr={VALUE}` can be replaced by `--set=service.telemetry.metrics.address={VALUE}`;
- Updated confighttp `ToClient` to support passing telemetry settings for instrumenting otlphttp exporter(#4449)
- Remove support to some arches and platforms from `ocb` (opentelemetry-collector-builder) (#4710)
- Remove deprecated legacy path ("v1/trace") support for otlp http receiver (#4720)
- Change the `service.NewDefaultConfigProvider` to accept a slice of location strings (#4727).

### 🚩 Deprecations 🚩

- Deprecate `configtelemetry.Level.Set()` (#4700)

### 🧰 Bug fixes 🧰

- Ensure Windows path (e.g: C:) is recognized as a file path (#4726)
- Fix structured logging issue for windows service (#4686)

### 💡 Enhancements 💡

- Expose experimental API `configmapprovider.NewExpandConverter()` (#4672)
- `service.NewConfigProvider`: copy slice argument, disallow changes from caller to the input slice (#4729)
- `confighttp` and `configgrpc`: New config option `include_metadata` to persist request metadata/headers in `client.Info.Metadata` (experimental) (#4547)
- Remove expand cases that cannot happen with config.Map (#4649)
- Add `max_request_body_size` to confighttp.HTTPServerSettings (#4677)
- Move `compression.go` into `confighttp.go` to internalize functions in `compression.go` file. (#4651)
  - create `configcompression` package to manage compression methods in `confighttp` and `configgrpc`
- Add support for cgroupv2 memory limit (#4654)
- Enable end users to provide multiple files for config location (#4727)

## v0.42.0 Beta

### 🛑 Breaking changes 🛑

- Remove `configmapprovider.NewInMemory()` (#4507)
- Disallow direct implementation of `configmapprovider.Retrieved` (#4577)
- `configauth`: remove interceptor functions from the ServerAuthenticator interface (#4583)
- Replace ConfigMapProvider and ConfigUnmarshaler in collector settings by one simpler ConfigProvider (#4590)
- Remove deprecated consumererror.Combine (#4597)
- Remove `configmapprovider.NewDefault`, `configmapprovider.NewExpand`, `configmapprovider.NewMerge` (#4600)
  - The merge functionality is now embedded into `service.NewConfigProvider` (#4637).
- Move `configtest.LoadConfig` and `configtest.LoadConfigAndValidate` to `servicetest` (#4606)
- Builder: Remove deprecated `include-core` flag (#4616)
- Collector telemetry level must now be accessed through an atomic function. (#4549)

### 💡 Enhancements 💡

- `confighttp`: add client-side compression support. (#4441)
  - Each exporter should remove `compression` field if they have and should use `confighttp.HTTPClientSettings`
- Allow more zap logger configs: `disable_caller`, `disable_stacktrace`, `output_paths`, `error_output_paths`, `initial_fields` (#1048)
- Allow the custom zap logger encoding (#4532)
- Collector self-metrics may now be configured through the configuration file. (#4069)
  - CLI flags for configuring self-metrics are deprecated and will be removed
    in a future release.
  - `service.telemetry.metrics.level` and `service.telemetry.metrics.address`
    should be used to configure collector self-metrics.
- `configauth`: add helpers to create new server authenticators. (#4558)
- Refactor `configgrpc` for compression methods (#4624)
- Add an option to allow `config.Map` conversion in the `service.ConfigProvider` (#4634)
- Added support to expose gRPC framework's logs as part of collector logs (#4501)
- Builder: Enable unmarshal exact to help finding hard to find typos #4644

### 🧰 Bug fixes 🧰

- Fix merge config map provider to close the watchers (#4570)
- Fix expand map provider to call close on the base provider (#4571)
- Fix correct the value of `otelcol_exporter_send_failed_requests` (#4629)
- `otlp` receiver: Fix legacy port cfg value override and HTTP server starting bug (#4631)

## v0.41.0 Beta

### 🛑 Breaking changes 🛑

- Remove reference to `defaultcomponents` in core and deprecate `include_core` flag (#4087)
- Remove `config.NewConfigMapFrom[File|Buffer]`, add testonly version (#4502)
- `configtls`: TLS 1.2 is the new default mininum version (#4503)
- `confighttp`: `ToServer` now accepts a `component.Host`, in line with gRPC's counterpart (#4514)
- CORS configuration for OTLP/HTTP receivers has been moved into a `cors:` block, instead of individual `cors_allowed_origins` and `cors_allowed_headers` settings (#4492)

### 💡 Enhancements 💡

- OTLP/HTTP receivers now support setting the `Access-Control-Max-Age` header for CORS caching. (#4492)
- `client.Info` pre-populated for all receivers using common helpers like `confighttp` and `configgrpc` (#4423)

### 🧰 Bug fixes 🧰

- Fix handling of corrupted records by persistent buffer (experimental) (#4475)

### 💡 Enhancements 💡

- Extending the contribution guide to help clarify what is acceptable defaults and recommendations.

## v0.40.0 Beta

### 🛑 Breaking changes 🛑

- Package `client` refactored (#4416) and auth data included in it (#4422). Final PR to be merged in the next release (#4423)
- Remove `pdata.AttributeMap.InitFromMap` (#4429)
- Updated configgrpc `ToDialOptions` to support passing providers to instrumentation library (#4451)
- Make state information propagation non-blocking on the collector (#4460)

### 💡 Enhancements 💡

- Add semconv 1.7.0 and 1.8.0 (#4452)
- Added `feature-gates` CLI flag for controlling feature gate state. (#4368)
- Add a default user-agent header to the OTLP/gRPC and OTLP/HTTP exporters containing collector build information (#3970)

## v0.39.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated config (already no-op) `ballast_size_mib` in memorylimiterprocessor (#4365)
- Remove `config.Receivers`, `config.Exporters`, `config.Processors`, and `config.Extensions`. Use map directly (#4344)
- Remove `component.BaseProcessorFactory`, use `processorhelper.NewFactory` instead (#4175)
- Force usage of `exporterhelper.NewFactory` to implement `component.ExporterFactory` (#4338)
- Force usage of `receiverhelper.NewFactory` to implement `component.ReceiverFactory` (#4338)
- Force usage of `extensionhelper.NewFactory` to implement `component.ExtensionFactory` (#4338)
- Move `service/parserprovider` package to `config/configmapprovider` (#4206)
  - Rename `MapProvider` interface to `Provider`
  - Remove `MapProvider` from helper names
- Renamed slice-valued `pdata` types and functions for consistency. (#4325)
  - Rename `pdata.AnyValueArray` to `pdata.AttributeValueSlice`
  - Rename `ArrayVal()` to `SliceVal()`
  - Rename `SetArrayVal()` to `SetSliceVal()`
- Remove `config.Pipeline.Name` (#4326)
- Rename `config.Mapprovider` as `configmapprovider.Provider` (#4337)
- Move `config.WatchableRetrieved` and `config.Retrieved` interfaces to `config/configmapprovider` package (#4337)
- Remove `config.Pipeline.InputDataType` (#4343)
- otlpexporter: Do not retry on PermissionDenied and Unauthenticated (#4349)
- Enable configuring collector metrics through service config file. (#4069)
  - New `service::telemetry::metrics` structure added to configuration
  - Existing metrics configuration CLI flags are deprecated and to be
    removed in the future.
  - `--metrics-prefix` is no longer operative; the prefix is determined by
    the value of `service.buildInfo.Command`.
  - `--add-instance-id` is no longer operative; an instance ID will always be added.
- Remove deprecated funcs `consumererror.As[Traces|Metrics|Logs]` (#4364)
- Remove support to expand env variables in default configs (#4366)

### 💡 Enhancements 💡

- Supports more compression methods(`snappy` and `zstd`) for configgrpc, in addition to current `gzip` (#4088)
- Moved the OpenTelemetry Collector Builder to core (#4307)

### 🧰 Bug fixes 🧰

- Fix AggregationTemporality and IsMonotonic when metric descriptors are split in the batch processor (#4389)

## v0.38.0 Beta

### 🛑 Breaking changes 🛑

- Removed `configauth.HTTPClientAuthenticator` and `configauth.GRPCClientAuthenticator` in favor of `configauth.ClientAuthenticator`. (#4255)
- Rename `parserprovider.MapProvider` as `config.MapProvider`. (#4178)
- Rename `parserprovider.Watchable` as `config.WatchableMapProvider`. (#4178)
- Remove deprecated no-op flags to setup Collector's logging "--log-level", "--log-profile", "--log-format". (#4213)
- Move `cmd/pdatagen` as internal package `model/internal/cmd/pdatagen`. (#4243)
- Use directly the ComponentID in configauth. (#4238)
- Refactor configauth, getters use the map instead of iteration. (#4234)
- Change scraperhelper to follow the recommended append model for pdata. (#4202)

### 💡 Enhancements 💡

- Update proto to 0.11.0. (#4209)
- Change pdata to use the newly added [Traces|Metrics|Logs]Data. (#4214)
- Add ExponentialHistogram field to pdata. (#4219)
- Make sure otlphttp exporter tests include TraceID and SpanID. (#4268)
- Use multimod tool in release process. (#4229)
- Change queue metrics to use opencensus metrics instead of stats, close to otel-go. (#4220)
- Make receiver data delivery guarantees explicit (#4262)
- Simplify unmarshal logic by adding more supported hooks. (#4237)
- Add unmarshaler for otlpgrpc.[*]Request and otlpgrp.[*]Response (#4215)

## v0.37.0 Beta

### 🛑 Breaking changes 🛑

- Move `configcheck.ValidateConfigFromFactories` as internal function in service package (#3876)
- Rename `configparser.Parser` as `config.Map` (#4075)
- Rename `component.DefaultBuildInfo()` to `component.NewDefaultBuildInfo()` (#4129)
- Rename `consumererror.Permanent` to `consumererror.NewPermanent` (#4118)
- Rename `config.NewID` to `config.NewComponentID` and `config.NewIDFromString` to `config.NewComponentIDFromString` (#4137)
- Rename `config.NewIDWithName` to `config.NewComponentIDWithName` (#4151)
- Move `extension/storage` to `extension/experimental/storage` (#4082)
- Rename `obsreporttest.SetupRecordedMetricsTest()` to `obsreporttest.SetupTelemetry()` and `obsreporttest.TestTelemetrySettings` to `obsreporttest.TestTelemetry` (#4157)

### 💡 Enhancements 💡

- Add Gen dependabot into CI (#4083)
- Update OTLP to v0.10.0 (#4045).
- Add Flags field to NumberDataPoint, HistogramDataPoint, SummaryDataPoint (#4081).
- Add feature gate library (#4108)
- Add version to the internal telemetry metrics (#4140)

### 🧰 Bug fixes 🧰

- Fix panic when not using `service.NewCommand` (#4139)

## v0.36.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated pdata.AttributeMapToMap (#3994)
- Move ValidateConfig from configcheck to configtest (#3956)
- Remove `mem-ballast-size-mib`, already deprecated and no-op (#4005)
- Remove `semconv.AttributeMessageType` (#4020)
- Remove `semconv.AttributeHTTPStatusText` (#4015)
- Remove squash on `configtls.TLSClientSetting` and move TLS client configs under `tls` (#4063)
- Rename TLS server config `*configtls.TLSServerSetting` from `tls_settings` to `tls` (#4063)
- Split `service.Collector` from the `cobra.Command` (#4074)
- Rename `memorylimiter` to `memorylimiterprocessor` (#4064)

### 💡 Enhancements 💡

- Create new semconv package for v1.6.1 (#3948)
- Add AttributeValueBytes support to AsString (#4002)
- Add AttributeValueTypeBytes support to AttributeMap.AsRaw (#4003)
- Add MeterProvider to TelemetrySettings (#4031)
- Add configuration to setup collector logs via config file. (#4009)

## v0.35.0 Beta

### 🛑 Breaking changes 🛑

- Remove the legacy gRPC port(`55680`) support in OTLP receiver (#3966)
- Rename configparser.Parser to configparser.ConfigMap (#3964)
- Remove obsreport.ScraperContext, embed into StartMetricsOp (#3969)
- Remove dependency on deprecated go.opentelemetry.io/otel/oteltest (#3979)
- Remove deprecated pdata.AttributeValueToString (#3953)
- Remove deprecated pdata.TimestampFromTime. Closes: #3925 (#3935)

### 💡 Enhancements 💡

- Add TelemetryCreateSettings (#3984)
- Only initialize collector telemetry once (#3918)
- Add trace context info to LogRecord log (#3959)
- Add new view for AWS ECS health check extension. (#3776)

## v0.34.0 Beta

### 🛑 Breaking changes 🛑

- Artifacts are no longer published in this repository, check [here](https://github.com/open-telemetry/opentelemetry-collector-releases) (#3941)
- Remove deprecated `tracetranslator.AttributeValueToString` and `tracetranslator.AttributeMapToMap` (#3873)
- Change semantic conventions for status (code, msg) as per specifications (#3872)
- Move `fileexporter` to contrib (#3474)
- Move `jaegerexporter` to contrib (#3474)
- Move `kafkaexporter` to contrib (#3474)
- Move `opencensusexporter` to contrib (#3474)
- Move `prometheusexporter` to contrib (#3474)
- Move `prometheusremotewriteexporter` to contrib (#3474)
- Move `zipkinexporter` to contrib (#3474)
- Move `attributeprocessor` to contrib (#3474)
- Move `filterprocessor` to contrib (#3474)
- Move `probabilisticsamplerprocessor` to contrib (#3474)
- Move `resourceprocessor` to contrib (#3474)
- Move `spanprocessor` to contrib (#3474)
- Move `hostmetricsreceiver` to contrib (#3474)
- Move `jaegerreceiver` to contrib (#3474)
- Move `kafkareceiver` to contrib (#3474)
- Move `opencensusreceiver` to contrib (#3474)
- Move `prometheusreceiver` to contrib (#3474)
- Move `zipkinreceiver` to contrib (#3474)
- Move `bearertokenauthextension` to contrib (#3474)
- Move `healthcheckextension` to contrib (#3474)
- Move `oidcauthextension` to contrib (#3474)
- Move `pprofextension` to contrib (#3474)
- Move `translator/internaldata` to contrib (#3474)
- Move `translator/trace/jaeger` to contrib (#3474)
- Move `translator/trace/zipkin` to contrib (#3474)
- Move `testbed` to contrib (#3474)
- Move `exporter/exporterhelper/resource_to_telemetry` to contrib (#3474)
- Move `processor/processorhelper/attraction` to contrib (#3474)
- Move `translator/conventions` to `model/semconv` (#3901)

### 🚩 Deprecations 🚩

- Add `pdata.NewTimestampFromTime`, deprecate `pdata.TimestampFromTime` (#3868)
- Add `pdata.NewAttributeMapFromMap`, deprecate `pdata.AttributeMap.InitFromMap` (#3936)

## v0.33.0 Beta

### 🛑 Breaking changes 🛑

- Rename `configloader` interface to `configunmarshaler` (#3774)
- Remove `LabelsMap` from all the metrics points (#3706)
- Update generated K8S attribute labels to fix capitalization (#3823)

### 💡 Enhancements 💡

- Collector has now full support for metrics proto v0.9.0.

## v0.32.0 Beta

This release is marked as "bad" since the metrics pipelines will produce bad data.

- See https://github.com/open-telemetry/opentelemetry-collector/issues/3824

### 🛑 Breaking changes 🛑

- Rename `CustomUnmarshable` interface to `Unmarshallable` (#3774)

### 💡 Enhancements 💡

- Change default OTLP/HTTP port number from 55681 to 4318 (#3743)
- Update OTLP proto to v0.9.0 (#3740)
  - Remove `SetValue`/`Value` func for `NumberDataPoint`/`Exemplar` (#3730)
  - Remove `IntGauge`/`IntSum`from pdata (#3731)
  - Remove `IntDataPoint` from pdata (#3735)
  - Add support for `Bytes` attribute type (#3756)
  - Add `SchemaUrl` field (#3759)
  - Add `Attributes` to `NumberDataPoint`, `HistogramDataPoint`, `SummaryDataPoint` (#3761)
- `conventions` translator: Replace with conventions generated from spec v1.5.0 (#3494)
- `prometheus` receiver: Add `ToMetricPdata` method (#3695)
- Make configsource `Watchable` an optional interface (#3792)
- `obsreport` exporter: Change to accept `ExporterCreateSettings` (#3789)

### 🧰 Bug fixes 🧰

- `configgrpc`: Use chained interceptors in the gRPC server (#3744)
- `prometheus` receiver: Use actual interval startTimeMs for cumulative types (#3694)
- `jaeger` translator: Fix bug that could generate empty proto spans (#3808)

## v0.31.0 Beta

### 🛑 Breaking changes 🛑

- Remove Resize() from pdata slice APIs (#3675)
- Remove the ballast allocation when `mem-ballast-size-mib` is set in command line (#3626)
  - Use [`ballast extension`](./extension/ballastextension/README.md) to set memory ballast instead.
- Rename `DoubleDataPoint` to `NumberDataPoint` (#3633)
- Remove `IntHistogram` (#3676)

### 💡 Enhancements 💡

- Update to OTLP 0.8.0:
  - Translate `IntHistogram` to `Histogram` in `otlp_wrappers` (#3676)
  - Translate `IntGauge` to `Gauge` in `otlp_wrappers` (#3619)
  - Translate `IntSum` to `Sum` in `otlp_wrappers` (#3621)
  - Update `NumberDataPoint` to support `DoubleVal` and `IntVal` (#3689)
  - Update `Exemplar` to use `oneOfPrimitiveValue` (#3699)
  - Remove `IntExemplar` and `IntExemplarSlice` from `pdata` (#3705)
  - Mark `IntGauge`/`IntSum`/`IntDataPoint` as deprecated (#3707)
  - Remove `IntGauge`/`IntSum` from `batchprocessor` (#3718)
  - `prometheusremotewrite` exporter: Convert to new Number metrics (#3714)
  - `prometheus` receiver: Convert to new Number metrics (#3716)
  - `prometheus` exporter: Convert to new Number metrics (#3709)
  - `hostmetrics` receiver: Convert to new Number metrics (#3710)
  - `opencensus`: Convert to new Number metrics (#3708)
  - `scraperhelper` receiver: Convert to new Number metrics (#3717)
  - `testbed`: Convert to new Number metrics (#3719)
  - `expoerterhelper`: Convert `resourcetolabel` to new Number metrics (#3723)
- `configauth`: Prepare auth API to return a context (#3618)
- `pdata`:
  - Implement `Equal()` for map-valued `AttributeValues` (#3612)
  - Add `[Type]Slice.Sort(func)` to sort slices (#3671)
- `memorylimiter`:
  - Add validation on ballast size between `memorylimiter` and `ballastextension` (#3532)
  - Access Ballast extension via `Host.GetExtensions` (#3634)
- `prometheusremotewrite` exporter: Add a WAL implementation without wiring up (#3597)
- `prometheus` receiver: Add `metricGroup.toDistributionPoint` pdata conversion (#3667)
- Use `ComponentID` as identifier instead of config (#3696)
- `zpages`: Move config validation from factory to `Validate` (#3697)
- Enable `tracez` z-pages from otel-go, disable opencensus (#3698)
- Convert temporality and monotonicity for deprecated sums (#3729)

### 🧰 Bug fixes 🧰

- `otlpexporter`: Allow endpoint to be configured with a scheme of `http` or `https` (#3575)
- Handle errors when reloading the collector service (#3615)
- Do not report fatal error when `cmux.ErrServerClosed` (#3703)
- Fix bool attribute equality in `pdata` (#3688)

## v0.30.0 Beta

### 🛑 Breaking changes 🛑

- Rename `pdata.DoubleSum` to `pdata.Sum` (#3583)
- Rename `pdata.DoubleGauge` to `pdata.Gauge` (#3599)
- Migrated `pdata` to a dedicated package (#3483)
- Change Marshaler/Unmarshaler to be consistent with other interfaces (#3502)
- Remove consumer/simple package (#3438)
- Remove unnecessary interfaces from pdata (#3506)
- zipkinv1 implement directly Unmarshaler interface (#3504)
- zipkinv2 implement directly Marshaler/Unmarshaler interface (#3505)
- Change exporterhelper to accept ExporterCreateSettings instead of just logger (#3569)
- Use Func pattern in processorhelper, consistent with others (#3570)

### 🚩 Deprecations 🚩

- Deprecate Resize() from pdata slice APIs (#3573)

### 💡 Enhancements 💡

- Update OTLP to v0.8.0 (#3572)
- Migrate from OpenCensus to OpenTelemetry for internal tracing (#3567)
- Move internal/pdatagrpc to model/otlpgrpc (#3507)
- Move internal/otlp to model/otlp (#3508)
- Create http Server via Config, enable cors and decompression (#3513)
- Allow users to set min and max TLS versions (#3591)
- Support setting ballast size in percentage of total Mem in ballast extension (#3456)
- Publish go.opentelemetry.io/collector/model as a separate module (#3530)
- Pass a TracerProvider via construct settings to all the components (#3592)
- Make graceful shutdown optional (#3577)

### 🧰 Bug fixes 🧰

- `scraperhelper`: Include the scraper name in log messages (#3487)
- `scraperhelper`: fix case when returned pdata is empty (#3520)
- Record the correct number of points not metrics in Kafka receiver (#3553)
- Validate the Prometheus configuration (#3589)

## v0.29.0 Beta

### 🛑 Breaking changes 🛑

- Rename `service.Application` to `service.Collector` (#3268)
- Provide case sensitivity in config yaml mappings by using Koanf instead of Viper (#3337)
- Move zipkin constants to an internal package (#3431)
- Disallow renaming metrics using metric relabel configs (#3410)
- Move cgroup and iruntime utils from memory_limiter to internal folder (#3448)
- Move model pdata interfaces to pdata, expose them publicly (#3455)

### 💡 Enhancements 💡

- Change obsreport helpers for scraper to use the same pattern as Processor/Exporter (#3327)
- Convert `otlptext` to implement Marshaler interfaces (#3366)
- Add encoder/decoder and marshaler/unmarshaler for OTLP protobuf (#3401)
- Use the new marshaler/unmarshaler in `kafka` exporter (#3403)
- Convert `zipkinv2` to to/from translator interfaces (#3409)
- `zipkinv1`: Move to translator and encoders interfaces (#3419)
- Use the new marshaler/unmarshaler in `kafka` receiver #3402
- Change `oltp` receiver to use the new unmarshaler, avoid grpc-gateway dependency (#3406)
- Use the new Marshaler in the `otlphttp` exporter (#3433)
- Add grpc response struct for all signals instead of returning interface in `otlp` receiver/exporter (#3437)
- `zipkinv2`: Add encoders, decoders, marshalers (#3426)
- `scrapererror` receiver: Return concrete error type (#3360)
- `kafka` receiver: Add metrics support (#3452)
- `prometheus` receiver:
  - Add store to track stale metrics (#3414)
  - Add `up` and `scrape_xxxx` internal metrics (#3116)

### 🧰 Bug fixes 🧰

- `prometheus` receiver:
  - Reject datapoints with duplicate label keys (#3408)
  - Scrapers are not stopped when receiver is shutdown (#3450)
- `prometheusremotewrite` exporter: Adjust default retry settings (#3416)
- `hostmetrics` receiver: Fix missing startTimestamp for `processes` scraper (#3461)

## v0.28.0 Beta

### 🛑 Breaking changes 🛑

- Remove unused logstest package (#3222)
- Introduce `AppSettings` instead of `Parameters` (#3163)
- Remove unused testutil.TempSocketName (#3291)
- Move BigEndian helper functions in `tracetranslator` to an internal package.(#3298)
- Rename `configtest.LoadConfigFile` to `configtest.LoadConfigAndValidate` (#3306)
- Replace `ExtensionCreateParams` with `ExtensionCreateSettings` (#3294)
- Replace `ProcessorCreateParams` with `ProcessorCreateSettings`. (#3181)
- Replace `ExporterCreateParams` with `ExporterCreateSettings` (#3164)
- Replace `ReceiverCreateParams` with `ReceiverCreateSettings`. (#3167)
- Change `batchprocessor` logic to limit data points rather than metrics (#3141)
- Rename `PrwExporter` to `PRWExporter` and `NewPrwExporter` to `NewPRWExporter` (#3246)
- Avoid exposing OpenCensus reference in public APIs (#3253)
- Move `config.Parser` to `configparser.Parser` (#3304)
- Remove deprecated funcs inside the obsreceiver (#3314)
- Remove `obsreport.GRPCServerWithObservabilityEnabled`, enable observability in config (#3315)
- Remove `obsreport.ProcessorMetricViews`, use `BuildProcessorCustomMetricName` where needed (#3316)
- Remove "Receive" from `obsreport.Receiver` funcs (#3326)
- Remove "Export" from `obsreport.Exporter` funcs (#3333)
- Hide unnecessary public struct `obsreport.StartReceiveOptions` (#3353)
- Avoid exposing internal implementation public in OC/OTEL receivers (#3355)
- Updated configgrpc `ToDialOptions` and confighttp `ToClient` apis to take extensions configuration map (#3340)
- Remove `GenerateSequentialTraceID` and `GenerateSequentialSpanIDin` functions in testbed (#3390)
- Change "grpc" to "GRPC" in configauth function/type names (#3285)

### 💡 Enhancements 💡

- Add `doc.go` files to the consumer package and its subpackages (#3270)
- Improve documentation of consumer package and subpackages (#3269, #3361)
- Automate triggering of doc-update on release (#3234)
- Enable Dependabot for Github Actions (#3312)
- Remove the proto dependency in `goldendataset` for traces (#3322)
- Add telemetry for dropped data due to exporter sending queue overflow (#3328)
- Add initial implementation of `pdatagrcp` (#3231)
- Change receiver obsreport helpers pattern to match the Processor/Exporter (#3227)
- Add model translation and encoding interfaces (#3200)
- Add otlpjson as a serializer implementation (#3238)
- `prometheus` receiver:
  - Add `createNodeAndResourcePdata` for Prometheus->OTLP pdata (#3139)
  - Direct metricfamily Prometheus->OTLP (#3145)
- Add `componenttest.NewNop*CreateSettings` to simplify tests (#3375)
- Add support for markdown generation (#3100)
- Refactor components for the Client Authentication Extensions (#3287)

### 🧰 Bug fixes 🧰

- Use dedicated `zapcore.Core` for Windows service (#3147)
- Hook up start and shutdown functions in fileexporter (#3260)
- Fix oc to pdata translation for sum non-monotonic cumulative (#3272)
- Fix `timeseriesSignature` in prometheus receiver (#3310)

## v0.27.0 Beta

### 🛑 Breaking changes 🛑

- Change `Marshal` signatures in kafkaexporter's Marshalers to directly convert pdata to `sarama.ProducerMessage` (#3162)
- Remove `tracetranslator.DetermineValueType`, only used internally by Zipkin (#3114)
- Remove OpenCensus conventions, should not be used (#3113)
- Remove Zipkin specific translation constants, move to internal (#3112)
- Remove `tracetranslator.TagHTTPStatusCode`, use `conventions.AttributeHTTPStatusCode` (#3111)
- Remove OpenCensus status constants and transformation (#3110)
- Remove `tracetranslator.AttributeArrayToSlice`, not used in core or contrib (#3109)
- Remove `internaldata.MetricsData`, same APIs as for traces (#3156)
- Rename `config.IDFromString` to `NewIDFromString`, remove `MustIDFromString` (#3177)
- Move consumerfanout package to internal (#3207)
- Canonicalize enum names in pdata. Fix usage of uppercase names (#3208)

### 💡 Enhancements 💡

- Use `config.ComponentID` for obsreport receiver/scraper (#3098)
- Add initial implementation of the consumerhelper (#3146)
- Add Collector version to Prometheus Remote Write Exporter user-agent header (#3094)
- Refactor processorhelper to use consumerhelper, split by signal type (#3180)
- Use consumerhelper for exporterhelper, add WithCapabilities (#3186)
- Set capabilities for all core exporters, remove unnecessary funcs (#3190)
- Add an internal sharedcomponent to be shared by receivers with shared resources (#3198)
- Allow users to configure the Prometheus remote write queue (#3046)
- Mark internaldata traces translation as deprecated for external usage (#3176)

### 🧰 Bug fixes 🧰

- Fix Prometheus receiver metric start time and reset determination logic. (#3047)
  - The receiver will no longer drop the first sample for `counter`, `summary`, and `histogram` metrics.
- The Prometheus remote write exporter will no longer force `counter` metrics to have a `_total` suffix. (#2993)
- Remove locking from jaeger receiver start and stop processes (#3070)
- Fix batch processor metrics reorder, improve performance (#3034)
- Fix batch processor traces reorder, improve performance (#3107)
- Fix batch processor logs reorder, improve performance (#3125)
- Avoid one unnecessary allocation in grpc OTLP exporter (#3122)
- `batch` processor: Validate that batch config max size is greater than send size (#3126)
- Add capabilities to consumer, remove from processor (#2770)
- Remove internal protos usage in Prometheusremotewrite exporter (#3184)
- `prometheus` receiver: Honor Prometheus external labels (#3127)
- Validate that remote write queue settings are not negative (#3213)

## v0.26.0 Beta

### 🛑 Breaking changes 🛑

- Change `With*Unmarshallers` signatures in Kafka exporter/receiver (#2973)
- Rename `marshall` to `marshal` in all the occurrences (#2977)
- Remove `componenterror.ErrAlreadyStarted` and `componenterror.ErrAlreadyStopped`, components should not protect against this, Service will start/stop once.
- Rename `ApplicationStartInfo` to `BuildInfo`
- Rename `ApplicationStartInfo.ExeName` to `BuildInfo.Command`
- Rename `ApplicationStartInfo.LongName` to `BuildInfo.Description`

### 🚩 Deprecations 🚩

- Add AppendEmpty and deprecate Append for slices (#2970)

### 💡 Enhancements 💡

- `kafka` exporter: Add logs support (#2943)
- Update mdatagen to create factories of init instead of new (#2978)
- `zipkin` receiver: Reduce the judgment of zipkin v1 version (#2990)
- Custom authenticator logic to accept a `component.Host` which will extract the authenticator to use based on a new authenticator name property (#2767)
- `prometheusremotewrite` exporter: Add `resource_to_telemetry_conversion` config option (#3031)
- `logging` exporter: Extract OTLP text logging (#3082)
- Format timestamps as strings instead of int in otlptext output (#3088)
- Add darwin arm64 build (#3090)

### 🧰 Bug fixes 🧰

- Fix Jaeger receiver to honor TLS Settings (#2866)
- `zipkin` translator: Handle missing starttime case for zipkin json v2 format spans (#2506)
- `prometheus` exporter: Fix OTEL resource label drops (#2899)
- `prometheusremotewrite` exporter:
  - Enable the queue internally (#2974)
  - Don't drop instance and job labels (#2979)
- `jaeger` receiver: Wait for server goroutines exit on shutdown (#2985)
- `logging` exporter: Ignore invalid handle on close (#2994)
- Fix service zpages (#2996)
- `batch` processor: Fix to avoid reordering and send max size (#3029)

## v0.25.0 Beta

### 🛑 Breaking changes 🛑

- Rename ForEach (in pdata) with Range to be consistent with sync.Map (#2931)
- Rename `componenthelper.Start` to `componenthelper.StartFunc` (#2880)
- Rename `componenthelper.Stop` to `componenthelper.StopFunc` (#2880)
- Remove `exporterheleper.WithCustomUnmarshaler`, `processorheleper.WithCustomUnmarshaler`, `receiverheleper.WithCustomUnmarshaler`, `extensionheleper.WithCustomUnmarshaler`, implement `config.CustomUnmarshaler` interface instead (#2867)
- Remove `component.CustomUnmarshaler` implement `config.CustomUnmarshaler` interface instead (#2867)
- Remove `testutil.HostPortFromAddr`, users can write their own parsing helper (#2919)
- Remove `configparser.DecodeTypeAndName`, use `config.IDFromString` (#2869)
- Remove `config.NewViper`, users should use `config.NewParser` (#2917)
- Remove `testutil.WaitFor`, use `testify.Eventually` helper if needed (#2920)
- Remove testutil.WaitForPort, users can use testify.Eventually (#2926)
- Rename `processorhelper.NewTraceProcessor` to `processorhelper.NewTracesProcessor` (#2935)
- Rename `exporterhelper.NewTraceExporter` to `exporterhelper.NewTracesExporter` (#2937)
- Remove InitEmptyWithCapacity, add EnsureCapacity and Clear (#2845)
- Rename traces methods/objects to include Traces in Kafka receiver (#2966)

### 💡 Enhancements 💡

- Add `validatable` interface with `Validate()` to all `config.<component>` (#2898)
  - add the empty `Validate()` implementation for all component configs
- **Experimental**: Add a config source manager that wraps the interaction with config sources (#2857, #2903, #2948)
- `kafka` exporter: Key jaeger messages on traceid (#2855)
- `scraperhelper`: Don't try to count metrics if scraper returns an error (#2902)
- Extract ConfigFactory in a ParserProvider interface (#2868)
- `prometheus` exporter: Allows Summary metrics to be exported to Prometheus (#2900)
- `prometheus` receiver: Optimize `dpgSignature` function (#2945)
- `kafka` receiver: Add logs support (#2944)

### 🧰 Bug fixes 🧰

- `prometheus` receiver:
  - Treat Summary and Histogram metrics without "\_sum" counter as valid metric (#2812)
  - Add `job` and `instance` as well-known labels (#2897)
- `prometheusremotewrite` exporter:
  - Sort Sample by Timestamp to avoid out of order errors (#2941)
  - Remove incompatible queued retry (#2951)
- `kafka` receiver: Fix data race with batchprocessor (#2957)
- `jaeger` receiver: Jaeger agent should not report ErrServerClosed (#2965)

## v0.24.0 Beta

### 🛑 Breaking changes 🛑

- Remove legacy internal metrics for memorylimiter processor, `spans_dropped` and `trace_batches_dropped` (#2841)
  - For `spans_dropped` use `processor/refused_spans` with `processor=memorylimiter`
- Rename pdata._.[Start|End]Time to pdata._.[Start|End]Timestamp (#2847)
- Rename pdata.DoubleExemplar to pdata.Exemplar (#2804)
- Rename pdata.DoubleHistogram to pdata.Histogram (#2797)
- Rename pdata.DoubleSummary to pdata.Summary (#2774)
- Refactor `consumererror` package (#2768)
  - Remove `PartialError` type in favor of signal-specific types
  - Rename `CombineErrors()` to `Combine()`
- Refactor `componenthelper` package (#2778)
  - Remove `ComponentSettings` and `DefaultComponentSettings()`
  - Rename `NewComponent()` to `New()`
- obsReport.NewExporter accepts a settings struct (#2668)
- Remove ErrorWaitingHost from `componenttest` (#2582)
- Move `config.Load` to `configparser.Load` (#2796)
- Remove `configtest.NewViperFromYamlFile()`, use `config.Parser.NewParserFromFile()` (#2806)
- Remove `config.ViperSubExact()`, use `config.Parser.Sub()` (#2806)
- Update LoadReceiver signature to remove unused params (#2823)
- Move `configerror.ErrDataTypeIsNotSupported` to `componenterror.ErrDataTypeIsNotSupported` (#2886)
- Rename`CreateTraceExporter` type to `CreateTracesExporter` in `exporterhelper` (#2779)
- Move `fluentbit` extension to contrib (#2795)
- Move `configmodels` to `config` (#2808)
- Move `fluentforward` receiver to contrib (#2723)

### 🚩 Deprecations 🚩

- Deprecate `consumetest.New[${SIGNAL}]Nop` in favor of `consumetest.NewNop` (#2878)
- Deprecate `consumetest.New[${SIGNAL}]Err` in favor of `consumetest.NewErr` (#2878)

### 💡 Enhancements 💡

- `batch` processor: - Support max batch size for logs (#2736)
- Use `Endpoint` for health check extension (#2782)
- Use `confignet.TCPAddr` for `pprof` and `zpages` extensions (#2829)
- Add watcher to values retrieved via config sources (#2803)
- Updates for cloud semantic conventions (#2809)
  - `cloud.infrastructure_service` -> `cloud.platform`
  - `cloud.zone` -> `cloud.availability_zone`
- Add systemd environment file for deb/rpm packages (#2822)
- Add validate interface in `configmodels` to force each component do configuration validation (#2802, #2856)
- Add `aws.ecs.task.revision` to semantic conventions list (#2816)
- Set unprivileged user to container image (#2838)
- Add New funcs for extension, exporter, processor config settings (#2872)
- Report metric about current size of the exporter retry queue (#2858)
- Allow adding new signals in `ProcessorFactory` by forcing everyone to embed `BaseProcessorFactory` (#2885)

### 🧰 Bug fixes 🧰

- `pdata.TracesFromOtlpProtoBytes`: Fixes to handle backwards compatibility changes in proto (#2798)
- `jaeger` receiver: Escape user input used in output (#2815)
- `prometheus` exporter: Ensure same time is used for updated time (#2745)
- `prometheusremotewrite` exporter: Close HTTP response body (#2875)

## v0.23.0 Beta

### 🛑 Breaking changes 🛑

- Move fanout consumers to fanoutconsumer package (#2615)
- Rename ExporterObsReport to Exporter (#2658)
- Rename ProcessorObsReport to Processor (#2657)
- Remove ValidateConfig and add Validate on the Config struct (#2665)
- Rename pdata Size to OtlpProtoSize (#2726)
- Rename [Traces|Metrics|Logs]Consumer to [Traces|Metrics|Logs] (#2761)
- Remove public access for `componenttest.Example*` components:
  - Users of these structs for testing configs should use the newly added `componenttest.Nop*` (update all components name in the config `example*` -> `nop` and use `componenttest.NopComponents()`).
  - Users of these structs for sink like behavior should use `consumertest.*Sink`.

### 💡 Enhancements 💡

- `hostmetrics` receiver: List labels along with respective metrics in metadata (#2662)
- `exporter` helper: Remove obsreport.ExporterContext, always add exporter name as a tag to the metrics (#2682)
- `jaeger` exporter: Change to not use internal data (#2698)
- `kafka` receiver: Change to not use internal data (#2697)
- `zipkin` receiver: Change to not use internal data (#2699)
- `kafka` exporter: Change to not use internal data (#2696)
- Ensure that extensions can be created and started multiple times (#2679)
- Use otlp request in logs wrapper, hide members in the wrapper (#2692)
- Add MetricsWrapper to dissallow access to internal representation (#2693)
- Add TracesWrapper to dissallow access to internal representation (#2721)
- Allow multiple OTLP receivers to be created (#2743)

### 🧰 Bug fixes 🧰

- `prometheus` exporter: Fix to work with standard labels that follow the naming convention of using periods instead of underscores (#2707)
- Propagate name and transport for `prometheus` receiver and exporter (#2680)
- `zipkin` receiver: Ensure shutdown correctness (#2765)

## v0.22.0 Beta

### 🛑 Breaking changes 🛑

- Rename ServiceExtension to just Extension (#2581)
- Remove `consumerdata.TraceData` (#2551)
- Move `consumerdata.MetricsData` to `internaldata.MetricsData` (#2512)
- Remove custom OpenCensus sematic conventions that have equivalent in otel (#2552)
- Move ScrapeErrors and PartialScrapeError to `scrapererror` (#2580)
- Remove support for deprecated unmarshaler `CustomUnmarshaler`, only `Unmarshal` is supported (#2591)
- Remove deprecated componenterror.CombineErrors (#2598)
- Rename `pdata.TimestampUnixNanos` to `pdata.Timestamp` (#2549)

### 💡 Enhancements 💡

- `prometheus` exporter: Re-implement on top of `github.com/prometheus/client_golang/prometheus` and add `metric_expiration` option
- `logging` exporter: Add support for AttributeMap (#2609)
- Add semantic conventions for instrumentation library (#2602)

### 🧰 Bug fixes 🧰

- `otlp` receiver: Fix `Shutdown()` bug (#2564)
- `batch` processor: Fix Shutdown behavior (#2537)
- `logging` exporter: Fix handling the loop for empty attributes (#2610)
- `prometheusremotewrite` exporter: Fix counter name check (#2613)

## v0.21.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated function `IsValid` from trace/span ID (#2522)
- Remove accessors for deprecated status code (#2521)

### 💡 Enhancements 💡

- `otlphttp` exporter: Add `compression` option for gzip encoding of outgoing http requests (#2502)
- Add `ScrapeErrors` struct to `consumererror` to simplify errors usage (#2414)
- Add `cors_allowed_headers` option to `confighttp` (#2454)
- Add SASL/SCRAM authentication mechanism on `kafka` receiver and exporter (#2503)

### 🧰 Bug fixes 🧰

- `otlp` receiver: Sets the correct deprecated status code before sending data to the pipeline (#2521)
- Fix `IsPermanent` to account for wrapped errors (#2455)
- `otlp` exporter: Preserve original error messages (#2459)

## v0.20.0 Beta

### 🛑 Breaking changes 🛑

- Rename `samplingprocessor/probabilisticsamplerprocessor` to `probabilisticsamplerprocessor` (#2392)

### 💡 Enhancements 💡

- `hostmetrics` receiver: Refactor to use metrics metadata utilities (#2405, #2406, #2421)
- Add k8s.node semantic conventions (#2425)

## v0.19.0 Beta

### 🛑 Breaking changes 🛑

- Remove deprecated `queued_retry` processor
- Remove deprecated configs from `resource` processor: `type` (set "opencensus.type" key in "attributes.upsert" map instead) and `labels` (use "attributes.upsert" instead).

### 💡 Enhancements 💡

- `hostmetrics` receiver: Refactor load metrics to use generated metrics (#2375)
- Add uptime to the servicez debug page (#2385)
- Add new semantic conventions for AWS (#2365)

### 🧰 Bug fixes 🧰

- `jaeger` exporter: Improve connection state logging (#2239)
- `pdatagen`: Fix slice of values generated code (#2403)
- `filterset` processor: Avoid returning always nil error in strict filterset (#2399)

## v0.18.0 Beta

### 🛑 Breaking changes 🛑

- Rename host metrics according to metrics spec and rename `swap` scraper to `paging` (#2311)

### 💡 Enhancements 💡

- Add check for `NO_WINDOWS_SERVICE` environment variable to force interactive mode on Windows (#2272)
- `hostmetrics` receiver: Add `disk/weighted_io_time` metric (Linux only) (#2312)
- `opencensus` exporter: Add queue-retry (#2307)
- `filter` processor: Filter metrics using resource attributes (#2251)

### 🧰 Bug fixes 🧰

- `fluentforward` receiver: Fix string conversions (#2314)
- Fix zipkinv2 translation error tag handling (#2253)

## v0.17.0 Beta

### 💡 Enhancements 💡

- Default config environment variable expansion (#2231)
- `prometheusremotewrite` exporter: Add batched exports (#2249)
- `memorylimiter` processor: Introduce soft and hard limits (#2250)

### 🧰 Bug fixes 🧰

- Fix nits in pdata usage (#2235)
- Convert status to not be a pointer in the Span (#2242)
- Report the error from `pprof.StartCPUProfile` (#2263)
- Rename `service.Application.SignalTestComplete` to `Shutdown` (#2277)

## v0.16.0 Beta

### 🛑 Breaking changes 🛑

- Rename Push functions to be consistent across signals in `exporterhelper` (#2203)

### 💡 Enhancements 💡

- Change default OTLP/gRPC port number to 4317, also continue receiving on legacy port
  55680 during transition period (#2104).
- `kafka` exporter: Add support for exporting metrics as otlp Protobuf. (#1966)
- Move scraper helpers to its own `scraperhelper` package (#2185)
- Add `componenthelper` package to help build components (#2186)
- Remove usage of custom init/stop in `scraper` and use start/shutdown from `component` (#2193)
- Add more trace annotations, so zpages are more useful to determine failures (#2206)
- Add support to skip TLS verification (#2202)
- Expose non-nullable metric types (#2208)
- Expose non-nullable elements from slices of pointers (#2200)

### 🧰 Bug fixes 🧰

- Change InstrumentationLibrary to be non-nullable (#2196)
- Add support for slices to non-pointers, use non-nullable AnyValue (#2192)
- Fix `--set` flag to work with `{}` in configs (#2162)

## v0.15.0 Beta

### 🛑 Breaking changes 🛑

- Remove legacy metrics, they were marked as legacy for ~12 months #2105

### 💡 Enhancements 💡

- Implement conversion between OpenCensus and OpenTelemetry Summary Metric (#2048)
- Add ability to generate non nullable messages (#2005)
- Implement Summary Metric in Prometheus RemoteWrite Exporter (#2083)
- Add `resource_to_telemetry_conversion` to exporter helper expose exporter settings (#2060)
- Add `CustomRoundTripper` function to httpclientconfig (#2085)
- Allow for more logging options to be passed to `service` (#2132)
- Add config parameters for `jaeger` receiver (#2068)
- Map unset status code for `jaegar` translator as per spec (#2134)
- Add more trace annotations to the queue-retry logic (#2136)
- Add config settings for component telemetry (#2148)
- Use net.SplitHostPort for IPv6 support in `prometheus` receiver (#2154)
- Add --log-format command line option (default to "console") #2177.

### 🧰 Bug fixes 🧰

- `logging` exporter: Add Logging for Summary Datapoint (#2084)
- `hostmetrics` receiver: use correct TCP state labels on Unix systems (#2087)
- Fix otlp_log receiver wrong use of trace measurement (#2117)
- Fix "process/memory/rss" metric units (#2112)
- Fix "process/cpu_seconds" metrics (#2113)
- Add check for nil logger in exporterhelper functions (#2141)
- `prometheus` receiver:
  - Upgrade Prometheus version to fix race condition (#2121)
  - Fix the scraper/discover manager coordination (#2089)
  - Fix panic when adjusting buckets (#2168)

## v0.14.0 Beta

### 🚀 New components 🚀

- `otlphttp` exporter which implements OTLP over HTTP protocol.

### 🛑 Breaking changes 🛑

- Rename consumer.TraceConsumer to consumer.TracesConsumer #1974
- Rename component.TraceReceiver to component.TracesReceiver #1975
- Rename component.TraceProcessor to component.TracesProcessor #1976
- Rename component.TraceExporter to component.TracesExporter #1975
- Move `tailsampling` processor to contrib (#2012)
- Remove NewAttributeValueSlice (#2028) and mark NewAttributeValue as deprecated (#2022)
- Remove pdata.StringValue (#2021)
- Remove pdata.InitFromAttributeMap, use CopyTo if needed (#2042)
- Remove SetMapVal and SetArrayVal for pdata.AttributeValue (#2039)

### 🚩 Deprecations 🚩

- Deprecate NopExporter, add NopConsumer (#1972)
- Deprecate SinkExporter, add SinkConsumer (#1973)

### 💡 Enhancements 💡

- `zipkin` exporter: Add queue retry to zipkin (#1971)
- `prometheus` exporter: Add `send_timestamps` option (#1951)
- `filter` processor: Add `expr` pdata.Metric filtering support (#1940, #1996)
- `attribute` processor: Add log support (#1934)
- `logging` exporter: Add index for histogram buckets count (#2009)
- `otlphttp` exporter: Add correct handling of server error responses (#2016)
- `prometheusremotewrite` exporter:
  - Add user agent header to outgoing http request (#2000)
  - Convert histograms to cumulative (#2049)
  - Return permanent errors (#2053)
  - Add external labels (#2044)
- `hostmetrics` receiver: Use scraper controller (#1949)
- Change Span/Trace ID to be byte array (#2001)
- Add `simple` metrics helper to facilitate building pdata.Metrics in receivers (#1540)
- Improve diagnostic logging for exporters (#2020)
- Add obsreport to receiverhelper scrapers (#1961)
- Update OTLP to 0.6.0 and use the new Span Status code (#2031)
- Add support of partial requests for logs and metrics to the exporterhelper (#2059)

### 🧰 Bug fixes 🧰

- `logging` exporter: Added array serialization (#1994)
- `zipkin` receiver: Allow receiver to parse string tags (#1893)
- `batch` processor: Fix shutdown race (#1967)
- Guard for nil data points (#2055)

## v0.13.0 Beta

### 🛑 Breaking changes 🛑

- Host metric `system.disk.time` renamed to `system.disk.operation_time` (#1887)
- Use consumer for sender interface, remove unnecessary receiver address from Runner (#1941)
- Enable sending queue by default in all exporters configured to use it (#1924)
- Removed `groupbytraceprocessor` (#1891)
- Remove ability to configure collection interval per scraper (#1947)

### 💡 Enhancements 💡

- Host Metrics receiver now reports both `system.disk.io_time` and `system.disk.operation_time` (#1887)
- Match spans against the instrumentation library and resource attributes (#928)
- Add `receiverhelper` for creating flexible "scraper" metrics receiver (#1886, #1890, #1945, #1946)
- Migrate `tailsampling` processor to new OTLP-based internal data model and add Composite Sampler (#1894)
- Metadata Generator: Change Metrics fields to implement an interface with new methods (#1912)
- Add unmarshalling for `pdata.Traces` (#1948)
- Add debug-level message on error for `jaeger` exporter (#1964)

### 🧰 Bug fixes 🧰

- Fix bug where the service does not correctly start/stop the log exporters (#1943)
- Fix Queued Retry Unusable without Batch Processor (#1813) - (#1930)
- `prometheus` receiver: Log error message when `process_start_time_seconds` gauge is missing (#1921)
- Fix trace jaeger conversion to internal traces zero time bug (#1957)
- Fix panic in otlp traces to zipkin (#1963)
- Fix OTLP/HTTP receiver's path to be /v1/traces (#1979)

## v0.12.0 Beta

### 🚀 New components 🚀

- `configauth` package with the auth settings that can be used by receivers (#1807, #1808, #1809, #1810)
- `perfcounters` package that uses perflib for host metrics receiver (#1835, #1836, #1868, #1869, #1870)

### 💡 Enhancements 💡

- Remove `queued_retry` and enable `otlp` metrics receiver in default config (#1823, #1838)
- Add `limit_percentage` and `spike_limit_percentage` options to `memorylimiter` processor (#1622)
- `hostmetrics` receiver:
  - Collect additional labels from partitions in the filesystems scraper (#1858)
  - Add filters for mount point and filesystem type (#1866)
- Add cloud.provider semantic conventions (#1865)
- `attribute` processor: Add log support (#1783)
- Introduce SpanID data type, not yet used in Protobuf messages ($1854, #1855)
- Enable `otlp` trace by default in the released docker image (#1883)
- `tailsampling` processor: Combine batches of spans into a single batch (#1864)
- `filter` processor: Update to use pdata (#1885)
- Allow MSI upgrades (#1914)

### 🚩 Deprecations 🚩

- Deprecate OpenCensus-based internal data structures (#1843)

### 🧰 Bug fixes 🧰

- `prometheus` receiver: Print a more informative message about 'up' metric value (#1826)
- Use custom data type and custom JSON serialization for traceid (#1840)
- Skip creation of redundant nil resource in translation from OC if there are no combined metrics (#1803)
- `tailsampling` processor: Only send to next consumer once (#1735)
- Report Windows pagefile usage in bytes (#1837)
- Fix issue where Prometheus SD config cannot be parsed (#1877)

## v0.11.0 Beta

### 🛑 Breaking changes 🛑

- Rename service.Start() to Run() since it's a blocking call
- Fix slice Append to accept by value the element in pdata
- Change CreateTraceProcessor and CreateMetricsProcessor to use the same parameter order as receivers/logs processor and exporters.
- Prevent accidental use of LogsToOtlp and LogsFromOtlp and the OTLP data structs (#1703)
- Remove SetType from configmodels, ensure all registered factories set the type in config (#1798)
- Move process telemetry to service/internal (#1794)

### 💡 Enhancements 💡

- Add map and array attribute value type support (#1656)
- Add authentication support to kafka (#1632)
- Implement InstrumentationLibrary translation to jaeger (#1645)
- Add public functions to export pdata to ExportXServicesRequest Protobuf bytes (#1741)
- Expose telemetry level in the configtelemetry (#1796)
- Add configauth package (#1807)
- Add config to docker image (#1792)

### 🧰 Bug fixes 🧰

- Use zap int argument for int values instead of conversion (#1779)
- Add support for gzip encoded payload in OTLP/HTTP receiver (#1581)
- Return proto status for OTLP receiver when failed (#1788)

## v0.10.0 Beta

### 🛑 Breaking changes 🛑

- **Update OTLP to v0.5.0, incompatible metrics protocol.**
- Remove support for propagating summary metrics in OtelCollector.
  - This is a temporary change, and will affect mostly OpenCensus users who use metrics.

### 💡 Enhancements 💡

- Support zipkin proto in `kafka` receiver (#1646)
- Prometheus Remote Write Exporter supporting Cortex (#1577, #1643)
- Add deployment environment semantic convention (#1722)
- Add logs support to `batch` and `resource` processors (#1723, #1729)

### 🧰 Bug fixes 🧰

- Identify config error when expected map is other value type (#1641)
- Fix Kafka receiver closing ready channel multiple times (#1696)
- Fix a panic issue while processing Zipkin spans with an empty service name (#1742)
- Zipkin Receiver: Always set the endtime (#1750)

## v0.9.0 Beta

### 🛑 Breaking changes 🛑

- **Remove old base factories**:
  - `ReceiverFactoryBase` (#1583)
  - `ProcessorFactoryBase` (#1596)
  - `ExporterFactoryBase` (#1630)
- Remove logs factories and merge with normal factories (#1569)
- Remove `reconnection_delay` from OpenCensus exporter (#1516)
- Remove `ConsumerOld` interfaces (#1631)

### 🚀 New components 🚀

- `prometheusremotewrite` exporter: Send metrics data in Prometheus TimeSeries format to Cortex or any Prometheus (#1544)
- `kafka` receiver: Receive traces from Kafka (#1410)

### 💡 Enhancements 💡

- `kafka` exporter: Enable queueing, retry, timeout (#1455)
- Add `Headers` field in HTTPClientSettings (#1552)
- Change OpenCensus receiver (#1556) and exporter (#1571) to the new interfaces
- Add semantic attribute for `telemetry.auto.version` (#1578)
- Add uptime and RSS memory self-observability metrics (#1549)
- Support conversion for OpenCensus `SameProcessAsParentSpan` (#1629)
- Access application version in components (#1559)
- Make Kafka payload encoding configurable (#1584)

### 🧰 Bug fixes 🧰

- Stop further processing if `filterprocessor` filters all data (#1500)
- `processscraper`: Use same scrape time for all data points coming from same process (#1539)
- Ensure that time conversion for 0 returns nil timestamps or Time where IsZero returns true (#1550)
- Fix multiple exporters panic (#1563)
- Allow `attribute` processor for external use (#1574)
- Do not duplicate filesystem metrics for devices with many mount points (#1617)

## v0.8.0 Beta

### 🚀 New components 🚀

- `groupbytrace` processor that waits for a trace to be completed (#1362)

### 💡 Enhancements 💡

- Migrate `zipkin` receiver/exporter to the new interfaces (#1484)
- Migrate `prometheus` receiver/exporter to the new interfaces (#1477, #1515)
- Add new FactoryUnmarshaler support to all components, deprecate old way (#1468)
- Update `fileexporter` to write data in OTLP (#1488)
- Add extension factory helper (#1485)
- Host scrapers: Use same scrape time for all data points coming from same source (#1473)
- Make logs SeverityNumber publicly available (#1496)
- Add recently included conventions for k8s and container resources (#1519)
- Add new config StartTimeMetricRegex to `prometheus` receiver (#1511)
- Convert Zipkin receiver and exporter to use OTLP (#1446)

### 🧰 Bug fixes 🧰

- Infer OpenCensus resource type based on OpenTelemetry's semantic conventions (#1462)
- Fix log adapter in `prometheus` receiver (#1493)
- Avoid frequent errors for process telemetry on Windows (#1487)

## v0.7.0 Beta

### 🚀 New components 🚀

- Receivers
  - `fluentfoward` runs a TCP server that accepts events via the [Fluent Forward protocol](https://github.com/fluent/fluentd/wiki/Forward-Protocol-Specification-v1) (#1173)
- Exporters
  - `kafka` exports traces to Kafka (#1439)
- Extensions
  - **Experimental** `fluentbit` facilitates running a FluentBit subprocess of the collector (#1381)

### 💡 Enhancements 💡

- Updated `golang/protobuf` from v1.3.5 to v1.4.2 (#1308)
- Updated `opencensus-proto` from v0.2.1 to v0.3.0 (#1308)
- Added round_robin `balancer_name` as an option to gRPC client settings (#1353)
- `hostmetrics` receiver
  - Switch to using perf counters to get disk io metrics on Windows (#1340)
  - Add device filter for file system (#1379) and disk (#1378) scrapers
  - Record process physical & virtual memory stats separately (#1403)
  - Scrape system.disk.time on Windows (#1408)
  - Add disk.pending_operations metric (#1428)
  - Add network interface label to network metrics (#1377)
- Add `exporterhelper` (#1351) and `processorhelper` (#1359) factories
- Update OTLP to latest version (#1384)
- Disable timeout, retry on failure and sending queue for `logging` exporter (#1400)
- Add support for retry and sending queue for `jaeger` exporter (#1401)
- Add batch size bytes metric to `batch` processor (#1270)
- `otlp` receiver: Add Log Support (#1444)
- Allow to configure read/write buffer sizes for http Client (#1447)
- Update DB conventions to latest and add exception conventions (#1452)

### 🧰 Bug fixes 🧰

- Fix `resource` processor for old metrics (#1412)
- `jaeger` receiver: Do not try to stop if failed to start. Collector service will do that (#1434)

## v0.6.0 Beta

### 🛑 Breaking changes 🛑

- Renamed the metrics generated by `hostmetrics` receiver to match the (currently still pending) OpenTelemetry system metric conventions (#1261) (#1269)
- Removed `vmmetrics` receiver (#1282)
- Removed `cpu` scraper `report_per_cpu` config option (#1326)

### 💡 Enhancements 💡

- Added disk merged (#1267) and process count (#1268) metrics to `hostmetrics`
- Log metric data points in `logging` exporter (#1258)
- Changed the `batch` processor to not ignore the errors returned by the exporters (#1259)
- Build and publish MSI (#1153) and DEB/RPM packages (#1278, #1335)
- Added batch size metric to `batch` processor (#1241)
- Added log support for `memorylimiter` processor (#1291) and `logging` exporter (#1298)
- Always add tags for `observability`, other metrics may use them (#1312)
- Added metrics support (#1313) and allow partial retries in `queued_retry` processor (#1297)
- Update `resource` processor: introduce `attributes` config parameter to specify actions on attributes similar to `attributes` processor, old config interface is deprecated (#1315)
- Update memory state labels for non-Linux OSs (#1325)
- Ensure tcp connection value is provided for all states, even when count is 0 (#1329)
- Set `batch` processor channel size to num cpus (#1330)
- Add `send_batch_max_size` config parameter to `batch` processor enforcing hard limit on batch size (#1310)
- Add support for including a per-RPC authentication to gRPC settings (#1250)

### 🧰 Bug fixes 🧰

- Fixed OTLP waitForReady, not set from config (#1254)
- Fixed all translation diffs between OTLP and Jaeger (#1222)
- Disabled `process` scraper for any non Linux/Windows OS (#1328)

## v0.5.0 Beta

### 🛑 Breaking changes 🛑

- **Update OTLP to v0.4.0 (#1142)**: Collector will be incompatible with any other sender or receiver of OTLP protocol
  of different versions
- Make "--new-metrics" command line flag the default (#1148)
- Change `endpoint` to `url` in Zipkin exporter config (#1186)
- Change `tls_credentials` to `tls_settings` in Jaegar receiver config (#1233)
- OTLP receiver config change for `protocols` to support mTLS (#1223)
- Remove `export_resource_labels` flag from Zipkin exporter (#1163)

### 🚀 New components 🚀

- Receivers
  - Added process scraper to the `hostmetrics` receiver (#1047)

### 💡 Enhancements 💡

- otlpexporter: send configured headers in request (#1130)
- Enable Collector to be run as a Windows service (#1120)
- Add config for HttpServer (#1196)
- Allow cors in HTTPServerSettings (#1211)
- Add a generic grpc server settings config, cleanup client config (#1183)
- Rely on gRPC to batch and loadbalance between connections instead of custom logic (#1212)
- Allow to tune the read/write buffers for gRPC clients (#1213)
- Allow to tune the read/write buffers for gRPC server (#1218)

### 🧰 Bug fixes 🧰

- Handle overlapping metrics from different jobs in prometheus exporter (#1096)
- Fix handling of SpanKind INTERNAL in OTLP OC translation (#1143)
- Unify zipkin v1 and v2 annotation/tag parsing logic (#1002)
- mTLS: Add support to configure client CA and enforce ClientAuth (#1185)
- Fixed untyped Prometheus receiver bug (#1194)
- Do not embed ProtocolServerSettings in gRPC (#1210)
- Add Context to the missing CreateMetricsReceiver method (#1216)

## v0.4.0 Beta

Released 2020-06-16

### 🛑 Breaking changes 🛑

- `isEnabled` configuration option removed (#909)
- `thrift_tchannel` protocol moved from `jaeger` receiver to `jaeger_legacy` in contrib (#636)

### ⚠️ Major changes ⚠️

- Switch from `localhost` to `0.0.0.0` by default for all receivers (#1006)
- Internal API Changes (only impacts contributors)
  - Add context to `Start` and `Stop` methods in the component (#790)
  - Rename `AttributeValue` and `AttributeMap` method names (#781)
    (other breaking changes in the internal trace data types)
  - Change entire repo to use the new vanityurl go.opentelemetry.io/collector (#977)

### 🚀 New components 🚀

- Receivers
  - `hostmetrics` receiver with CPU (#862), disk (#921), load (#974), filesystem (#926), memory (#911), network (#930), and virtual memory (#989) support
- Processors
  - `batch` for batching received metrics (#1060)
  - `filter` for filtering (dropping) received metrics (#1001)

### 💡 Enhancements 💡

- `otlp` receiver implement HTTP X-Protobuf (#1021)
- Exporters: Support mTLS in gRPC exporters (#927)
- Extensions: Add `zpages` for service (servicez, pipelinez, extensions) (#894)

### 🧰 Bug fixes 🧰

- Add missing logging for metrics at `debug` level (#1108)
- Fix setting internal status code in `jaeger` receivers (#1105)
- `zipkin` export fails on span without timestamp when used with `queued_retry` (#1068)
- Fix `zipkin` receiver status code conversion (#996)
- Remove extra send/receive annotations with using `zipkin` v1 (#960)
- Fix resource attribute mutation bug when exporting in `jaeger` proto (#907)
- Fix metric/spans count, add tests for nil entries in the slices (#787)

### 🧩 Components 🧩

#### Traces

| Receivers  |   Processors   | Exporters  |
|:----------:|:--------------:|:----------:|
|   Jaeger   |   Attributes   |    File    |
| OpenCensus |     Batch      |   Jaeger   |
|    OTLP    | Memory Limiter |  Logging   |
|   Zipkin   |  Queued Retry  | OpenCensus |
|            |    Resource    |    OTLP    |
|            |    Sampling    |   Zipkin   |
|            |      Span      |            |

#### Metrics

|  Receivers  |   Processors   | Exporters  |
|:-----------:|:--------------:|:----------:|
| HostMetrics |     Batch      |    File    |
| OpenCensus  |     Filter     |  Logging   |
|    OTLP     | Memory Limiter | OpenCensus |
| Prometheus  |                |    OTLP    |
| VM Metrics  |                | Prometheus |

#### Extensions

- Health Check
- Performance Profiler
- zPages

## v0.3.0 Beta

Released 2020-03-30

### Breaking changes

- Make prometheus receiver config loading strict. #697
  Prometheus receiver will now fail fast if the config contains unused keys in it.

### Changes and fixes

- Enable best effort serve by default of Prometheus Exporter (https://github.com/orijtech/prometheus-go-metrics-exporter/pull/6)
- Fix null pointer exception in the logging exporter #743
- Remove unnecessary condition to have at least one processor #744

### Components

| Receivers / Exporters |   Processors   |      Extensions      |
|:---------------------:|:--------------:|:--------------------:|
|        Jaeger         |   Attributes   |     Health Check     |
|      OpenCensus       |     Batch      | Performance Profiler |
|     OpenTelemetry     | Memory Limiter |        zPages        |
|        Zipkin         |  Queued Retry  |                      |
|                       |    Resource    |                      |
|                       |    Sampling    |                      |
|                       |      Span      |                      |

## v0.2.8 Alpha

Alpha v0.2.8 of OpenTelemetry Collector

- Implemented OTLP receiver and exporter.
- Added ability to pass config to the service programmatically (useful for custom builds).
- Improved own metrics / observability.
- Refactored component and factory interface definitions (breaking change #683)

## v0.2.7 Alpha

Alpha v0.2.7 of OpenTelemetry Collector

- Improved error handling on shutdown
- Partial implementation of new metrics (new obsreport package)
- Include resource labels for Zipkin exporter
- New `HASH` action to attribute processor

## v0.2.6 Alpha

Alpha v0.2.6 of OpenTelemetry Collector.

- Update metrics prefix to `otelcol` and expose command line argument to modify the prefix value.
- Extend Span processor to have include/exclude span logic.
- Batch dropped span now emits zero when no spans are dropped.

## v0.2.5 Alpha

Alpha v0.2.5 of OpenTelemetry Collector.

- Regexp-based filtering of spans based on service names.
- Ability to choose strict or regexp matching for include/exclude filters.

## v0.2.4 Alpha

Alpha v0.2.4 of OpenTelemetry Collector.

- Regexp-based filtering of span names.
- Ability to extract attributes from span names and rename span.
- File exporter for debugging.
- Span processor is now enabled by default.

## v0.2.3 Alpha

Alpha v0.2.3 of OpenTelemetry Collector.

Changes:
21a70d6 Add a memory limiter processor (#498)
9778b16 Refactor Jaeger Receiver config (#490)
ec4ad0c Remove workers from OpenCensus receiver implementation (#497)
4e01fa3 Update k8s config to use opentelemetry docker image and configuration (#459)

## v0.2.2 Alpha

Alpha v0.2.2 of OpenTelemetry Collector.

Main changes visible to users since previous release:

- Improved Testbed and added more E2E tests.
- Made component interfaces more uniform (this is a breaking change).

Note: v0.2.1 never existed and is skipped since it was tainted in some dependencies.

## v0.2.0 Alpha

Alpha v0.2 of OpenTelemetry Collector.

Docker image: omnition/opentelemetry-collector:v0.2.0 (we are working on getting this under an OpenTelemetry org)

Main changes visible to users since previous release:

- Rename from `service` to `collector`, the binary is now named `otelcol`

- Configuration reorganized and using strict mode

- Concurrency issues for pipelines transforming data addressed

Commits:

```terminal
0e505d5 Refactor config: pipelines now under service (#376)
402b80c Add Capabilities to Processor and use for Fanout cloning decision (#374)
b27d824 Use strict mode to read config (#375)
d769eb5 Fix concurrency handling when data is fanned out (#367)
dc6b290 Rename all github paths from opentelemtry-service to opentelemetry-collector (#371)
d038801 Rename otelsvc to otelcol (#365)
c264e0e Add Include/Exclude logic for Attributes Processor (#363)
8ce427a Pin a commit for Prometheus dependency in go.mod (#364)
2393774 Bump Jaeger version to 1.14.0 (latest) (#349)
63362d5 Update testbed modules (#360)
c0e2a27 Change dashes to underscores to separate words in config files (#357)
7609eaa Rename OpenTelemetry Service to Collector in docs and comments (#354)
bc5b299 Add common gRPC configuration settings (#340)
b38505c Remove network access popups on macos (#348)
f7727d1 Fixed loop variable pointer bug in jaeger translator (#341)
958beed Ensure that ConsumeMetricsData() is not passed empty metrics in the Prometheus receiver (#345)
0be295f Change log statement in Prometheus receiver from info to debug. (#344)
d205393 Add Owais to codeowners (#339)
8fa6afe Translate OC resource labels to Jaeger process tags (#325)
```

## v0.0.2 Alpha

Alpha release of OpenTelemetry Service.

Docker image: omnition/opentelemetry-service:v0.0.2 (we are working on getting this under an OpenTelemetry org)

Main changes visible to users since previous release:

```terminal
8fa6afe Translate OC resource labels to Jaeger process tags (#325)
047b0f3 Allow environment variables in config (#334)
96c24a3 Add exclude/include spans option to attributes processor (#311)
4db0414 Allow metric processors to be specified in pipelines (#332)
c277569 Add observability instrumentation for Prometheus receiver (#327)
f47aa79 Add common configuration for receiver tls (#288)
a493765 Refactor extensions to new config format (#310)
41a7afa Add Span Processor logic
97a71b3 Use full name for the metrics and spans created for observability (#316)
fed4ed2 Add support to record metrics for metricsexporter (#315)
5edca32 Add include_filter configuration to prometheus receiver (#298)
0068d0a Passthrough CORS allowed origins (#260)
```

## v0.0.1 Alpha

This is the first alpha release of OpenTelemetry Service.

Docker image: omnition/opentelemetry-service:v0.0.1

[v0.3.0]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.10...v0.3.0
[v0.2.10]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.8...v0.2.10
[v0.2.8]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.7...v0.2.8
[v0.2.7]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.6...v0.2.7
[v0.2.6]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.5...v0.2.6
[v0.2.5]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.4...v0.2.5
[v0.2.4]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.3...v0.2.4
[v0.2.3]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.2...v0.2.3
[v0.2.2]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.2.0...v0.2.2
[v0.2.0]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.0.2...v0.2.0
[v0.0.2]: https://github.com/open-telemetry/opentelemetry-collector/compare/v0.0.1...v0.0.2
[v0.0.1]: https://github.com/open-telemetry/opentelemetry-collector/tree/v0.0.1
