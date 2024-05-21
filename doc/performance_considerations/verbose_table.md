
Verbose Message Catalogue {#dev_guide_verbose_table}
========================================================

The following catalogue lists verbose messages, explanations, and additional information for: primitive creation and dispatch checks for primitive implementations; and implementation failures that occur during engine/memory object creation.

## Primitive Creation/Dispatching

| VERBOSE MESSAGE                                                       | SUBSTRING | PRIMITIVE   | EXPLANATION   |
|:----------------------------------------------------------------------|:----------|:------------|:--------------|
|**Bad/Invalid Arguments**                                              |           |             |               |         |
|`bad algorithm`                                                        |           | all         | Bad or invalid algorithm [`dnnl::algorithm`](https://oneapi-src.github.io/oneDNN/enum_dnnl_algorithm.html) selected for the current primitive implementation. The choice and availability of the algorithm depends on the specific implementation selected for the primitive. For example, oneDNN supports Winograd convolution only on GPU and AArch64 CPU systems. |
|`bad propagation kind`	                                                |           | all	       | Incorrect propagation kind [`dnnl::prop_kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_prop_kind.html) (`forward_training`,`backward_weights`, `backward_data`, etc.) selected for the current primitive implementation. |
|`bad param <p>`	                                                    |`p` - initialization parameter for [`dnnl::primitive_desc`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive_desc-2.html)           | all	        | Invalid parameter passed for the initialization of the primitive descriptor. <br/>**Example**: For the [`group_normalization`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_group_normalization.html) primitive, this message is displayed when the value passed for the `groups` parameter does not evenly divide the number of channels for the source tensor.             |
|`one of the mandatory arguments is nullptr`	                        |           | all	        | A NULL pointer argument exception for the primitive methods.         |
|`bad flags`	                                                        |           | all	        | Bad or unsupported flags specified for the primitive attributes [`dnnl::primitive_attr`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive_attr-2.html) during initialization of the primitive descriptor [`dnnl::primitive_desc`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive_desc-2.html).             |
|**Unsupported Arguments/Parameters**||||
|`unsupported isa`	                                                    |           | all	        | Primitive implementation does not support the current ISA. This typically results in the dispatching of the next best supporting implementation for the ISA.|
|`unsupported datatype`	                                                |           | all	        | Tensor datatype is not supported for the current implementation of the primitive. Depending on the primitive, this may correspond to the source, weight, bias or destination tensors.|
|`unsupported datatype combination`	                                    |           | all	        | Datatype combination for source, weight, bias or destination tensors is not supported for the current primitive implementation.  |
|`unsupported attr`	                                                    |           | all	        | Bad or unsupported attributes [`dnnl::primitive_attr`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive_attr-2.html) passed to the primitive descriptor for the current implementation. Since attributes are separately created from the corresponding primitive descriptor, the selected primitive implementation may not support the attribute configuration. |
|`unsupported post-ops`	                                                |           | all	        | Unsupported post-ops configuration [`dnnl::post_ops`](https://oneapi-src.github.io/oneDNN/struct_dnnl_post_ops-2.html) passed on to the primitive descriptor. Similar to `dnnl::primitive_attr`, the selected implementation may not support the postop configuration during primitve creation.|
|`unsupported scales configuration`	                                    |           | all	        | Unsupported scales configuration specified for the primitive attributes [`dnnl::primitive_attr`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive_attr-2.html). |
|`unsupported zero-point configuration`	                                |           | all	        | Unsupported zero-point configuration specified for the primitive attributes [`dnnl::primitive_attr`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive_attr-2.html).|
|`unsupported bias configuration`	                                    |           | all	        | Unsupported bias data configuration specified for the descriptors of compute-type primitives.|
|`unsupported sparse md configuration`	                                |           | all	        | Current primitive implementation does not support sparse data operations. |
|`unsupported format tag`	                                            |           | all	        | Unsupported format tag [`dnnl::memory::format_tag`](https://oneapi-src.github.io/oneDNN/enum_dnnl_memory_format_tag.html) encountered during primitive operation.|
|`unsupported format tag for <t>`	                                    |`t` - tensor         | all	        | Unsupported format tag [`dnnl::memory::format_tag`](https://oneapi-src.github.io/oneDNN/enum_dnnl_memory_format_tag.html) for specified tensor during primitive operation.|
|`unsupported format kind`	                                            |           | all	        | Unsupported format kind [`dnnl::memory::format_kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_memory_format_kind.html?highlight=format_kind) encountered during primitive operation.|
|`runtime dimension is not supported`	                                |           | all	        | Current implementation does not support processing runtime-specified shapes and strides using `DNNL_RUNTIME_DIM_VAL`. |
|**Tensor Operations**||||
|`tensor <t> has no elements`                                           |`t` - tensor          | all	        | Empty tensor passed as data to the primitive. Depending on the primitive, this may correspond to the source, weights or destination tensors.     |
|`<t> has a bad number of dimensions <ndims>`	                        |`t`- tensor<br/>`ndims`- number of tensor dimensions                     | all	        | Tensor data has bad or invalid number of dimensions for the current primitive operation.<br/>**Example**: The [`convolution`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_convolution.html) primitive expects only 1D, 2D or 3D tensors for operations and prints this message for any other data with higher dimensions.              |
|`bad dimensions <t>:<axis>`	                                        |`t`- tensor<br/>`axis`- axis          | all	        | Tensor `<t>` has an invalid dimension along the specified axis.<br/>**Example**: The [`concat`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_concat.html) primitive prints this message when the destination tensor dimension along the concatenated axis does not match the sum of the dimensions of the concatenated tensors.          |
|`dimension <t0>:<a0> is inconsistent with <t1>:<a1>`	                |`t0, t1` - tensors, <br/>`a0, a1` - tensor axes         | all	        | Tensors `t0, t1` have inconsistent dimensions along axes `a0` and `a1` respectively.<br/>**Example**: This is encountered for the [`matmul`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_matmul.html) primitive when the input matrices have mismatching dimensions.  |
|`tensors <t0> and <t1> have inconsistent number of dimensions`	        |`t0, t1` - tensors      | all	        |Tensors `t0, t1` have inconsistent dimensions for primitive operation.|
|`tensors <t0> and <t1> have inconsistent datatypes`	                |`t0, t1` - tensors     | all	        | Tensors `t0, t1` have inconsistent datatypes for primitive operation.|
|**Unsupported Combinations**||||
|`sparse encoding is not supported on this isa`	                        |           | all	        | *(self-explanatory)* |
|`datatype configuration not supported on this isa`	                    |           | all	        | *(self-explanatory)*|
|`datatype and propagation kind mismatch`	                            |           | all	        | *(self-explanatory)*|
|`inconsistent <t0> and <t1> mds`	                                    |`t0, t1` - tensors | all	        | Tensors `t0, t1` have inconsistent memory descriptors [`dnnl::memory::desc`](https://oneapi-src.github.io/oneDNN/struct_dnnl_memory_desc-2.html) for the primitive operation. |
|**Implementation Heuristics/Features**||||
|`unsupported feature for implementation: <msg>`                        |`msg` - feature description        | all	        | Current implementation is skipped because it does not support the specified feature for primtive operation. |
|`<msg> feature unavailable for device`	                                |`msg` - feature description         | all	        | Current implementation is skipped because the selected device does not support the specified feature for primitive operation.|
|`unsupported feature for padding: <msg>`	                            |`msg` - feature description         | all	        | Current implementation is skipped because of a padding inconsistency or unsupported feature related to padding.|
|`heuristic fail: <h>`	                                                |`h` - implementation heuristic           | all	        | Implementation skipped due to specified heuristic.|
|`blocking heuristic fail: <h>`	                                        |`h` - implementation  heuristic         | all	        | Current implementation is skipped because of the specified inconsistency or implementation heuristic related to blocking. |
|**Primitive-Specific Messages**||||
|`heuristic fail for 1x1 convolution: <h>`	                            |`h` - implementation heuristic          | [`convolution`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_convolution.html)	        | Implementation skipped due to specified heuristic related to 1x1 convolution.|
|`<o> offsets do not fit into <dt> datatype`	                        |`o` - {`input`, `output`},<br/>`dt` - datatype          | [`convolution`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_convolution.html)	        | I/O dimension offsets do not fit into the specified datatype range for the kernel implementation. |
|`failed shape restrictions`	                                        |           | [`convolution`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_convolution.html), [`gnorm`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_group_normalization.html) 	        |Implementation skipped because the current data layout/shapes exceeds the range supported by the current implementation.|
|`alpha and beta parameters are not properly set`	                    |           | [`eltwise`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_eltwise.html)	        | Alpha and beta parameters are not properly set for the elementwise algorithm. |
|`large shapes fall back`	                                            |           | [`gemm`](https://oneapi-src.github.io/oneDNN/dev_guide_convolution.html?highlight=gemm#algorithms)	        | Heuristic to skip current implementation for large tensor shapes for better performance.|
|`only trivial strides are supported`	                                |           | [`gemm`](https://oneapi-src.github.io/oneDNN/dev_guide_convolution.html?highlight=gemm#algorithms), [`rnn`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_rnn.html)	        | Current implementation for the primitive does not process non-trivial stride values.|
|`unsupported fpmath mode`	                                            |           | [`matmul`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_matmul.html)	        | [Floating-point math mode](https://oneapi-src.github.io/oneDNN/group_dnnl_api_fpmath_mode.html?highlight=math%20mode) is not supported by the current primitive implementation.|
|`small shapes fall back`	                                            |           | [`matmul`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_matmul.html)	        | Heuristic to skip current implementation for small tensor shapes for better performance. |
|`incompatible gemm format`	                                            |           | [`matmul`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_matmul.html), [`ip`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_inner_product.html)	        | Specified GeMM format is incompatible with the current primitive implementation.|
|`unsupported <t> tensor layout`	                                    |           | [`reorder`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_reorder.html)	         | The data layout for the source/destination tensor is not supported by the current implementation.|
|`bad axis`	                                                            |           | [`softmax`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_softmax.html), [`shuffle`](https://oneapi-src.github.io/oneDNN/group_dnnl_api_shuffle.html)	        | Bad or invalid axis specified for softmax/shuffle operation.             |
|`unsupported <d> architecture`	                       | `d` - [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html)                    | [`gemm`](https://oneapi-src.github.io/oneDNN/dev_guide_convolution.html?highlight=gemm#algorithms)	        | Unsupported architecture for specified device-type. Typically encountered when current GPU device does not support the primitive.|
|**Miscellaneous**||||
|`failed to create nested primitive <pm>`	                            |`pm` - [`dnnl::primitive`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive-2.html)     | all	        | Descriptor initialization for the nested primitive implementation was unsuccessful. |
|`failed to create <pm> descriptor`	                                |`pm` -[`dnnl::primitive`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive-2.html), [`dnnl::memory`](https://oneapi-src.github.io/oneDNN/struct_dnnl_memory-2.html)         | all	        | Descriptor initialization for the primitive or memory object was unsuccessful.|
|`bad accumulation mode`	                                            |           | all	        | Bad or invalid [accumulation mode](https://oneapi-src.github.io/oneDNN/enum_dnnl_accumulation_mode.html) specified for primitive attribute [`dnnl::primitive_attr`](https://oneapi-src.github.io/oneDNN/struct_dnnl_primitive_attr-2.html).             |
|`unsupported <t> md flag`	                                            |`t` - tensor          | all	        | Bad or unsupported flags specified for the memory descriptor [`dnnl::memory::desc`](https://oneapi-src.github.io/oneDNN/struct_dnnl_memory_desc-2.html).              |
|`problem is not mathematically consistent`	                            |           | all	        | *(self-explanatory)* |
|`workspace mismatch between forward and backward primitive descriptors`|           | all	        | *(self-explanatory)*|
|`workspace initialization failed`	                                    |           | all	        | [Workspace](https://oneapi-src.github.io/oneDNN/dev_guide_inference_and_training_aspects.html?highlight=workspace#workspace) descriptor initialization was unsuccessful during primitive creation.|
|`invalid datatype for <t>`	                                            |`t` - tensor          | all	        | The datatype for the tensor/data processed by the primitive is invalid. <br/> **Example**: This is encountered when an undefined datatype `data_type::undef` is specified for the accumulator.|
|`failed to run kernel deterministically`	                            |                      | all	        | failed to run application in the [deterministic mode](https://oneapi-src.github.io/oneDNN/dev_guide_attributes_deterministic.html?highlight=deterministic). |
|||||

## Engine Creation

| VERBOSE MESSAGE                                      | SUBSTRING | ENGINE      | EXPLANATION   |
|:-----------------------------------------------------|:----------|:------------|:--------------|
|`bad engine kind`                                     |           | all	     | Invalid value for [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html) encountered during engine creation.              |
|`invalid <d> device in environment: index <i>`        |`d` - [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html),<br/>`i` - device index           | all	     | Device of type `dnnl::engine::kind` and index `i` is invalid for the current environment.            |
|`no <d> device is available`           	           |`d` - [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html)          | all	     | No device of type `dnnl::engine::kind` was found during engine creation.              |
|`<n> <d> devices are available but <i> was queried`   |`d` - [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html), <br/>`n` - number of `d` devices,<br/>`i` - queried device index         | all	     | Queried index is out-of-range for device of type `dnnl::engine::kind`.               |
|`device not found in the given context`	           |           | all	     | *(self-explanatory)*              |
|`unsupported <d> platform (expected <d0> got <d1>)`  |`d` - [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html),<br/>`d0` - queried platform,<br/>`d1` - available platform           | `sycl`, `opencl`	     | Unsupported device platform encountered during engine creation.              |
|`failed to create <d> engine with index <i>`	       |`d` - [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html),<br/>`i` - device index              |all	     | Engine creation was unsuccessful for specified device index and kind.                |
|`unsupported <d> backend`	                           |`d` - [`dnnl::engine::kind`](https://oneapi-src.github.io/oneDNN/enum_dnnl_engine_kind.html)         | `sycl`	        | *(self-explanatory)*  |
|`profiling capabilities are not supported`	                            |           | all	        | Experimental profiling ([ONEDNN_EXPERIMENTAL_PROFILING](https://oneapi-src.github.io/oneDNN/dev_guide_experimental.html?highlight=profiling#onednn-experimental-profiling)) is not enabled for the application.|
|||||

## Memory Creation and Related Operations

| VERBOSE MESSAGE                           | EXPLANATION   |
|:------------------------------------------|:--------------|
|`bad arguments for memory descriptor`	    | Bad or unsupported values passed to the memory descriptor [`dnnl::memory::desc`](https://oneapi-src.github.io/oneDNN/struct_dnnl_memory_desc-2.html) during memory object creation.               |
|`invalid memory index`	                    | An out-of-range value encountered for memory handle during data mapping.              |
|`unsupported memory stride`	            | Memory descriptor initialization failed due to unsupported value for memory strides.               |
|`scratchpad memory limit exceeded`	        | [Scratchpad](https://oneapi-src.github.io/oneDNN/dev_guide_attributes_scratchpad.html?highlight=scratchpad) space is exhausted during GEMM kernel initialization.              |
|`scratchpad initialization unsuccessful`	| *(self-explanatory)*              |
|||||