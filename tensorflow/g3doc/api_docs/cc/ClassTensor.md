#Class tensorflow::Tensor

Represents an n-dimensional array of values.



##Member Summary

* [tensorflow::Tensor::Tensor](#tensorflow_Tensor_Tensor)
  * Default Tensor constructor. Creates a 1-dimension, 0-element float tensor.
* [tensorflow::Tensor::Tensor](#tensorflow_Tensor_Tensor)
  * Creates a Tensor of the given datatype and shape.
* [tensorflow::Tensor::Tensor](#tensorflow_Tensor_Tensor)
  * Creates a tensor with the input datatype and shape, using the allocator &apos;a&apos; to allocate the underlying buffer.
* [tensorflow::Tensor::Tensor](#tensorflow_Tensor_Tensor)
  * Creates an uninitialized Tensor of the given data type.
* [tensorflow::Tensor::Tensor](#tensorflow_Tensor_Tensor)
* [tensorflow::Tensor::~Tensor](#tensorflow_Tensor_Tensor)
  * Copy constructor.
* [DataType tensorflow::Tensor::dtype](#DataType_tensorflow_Tensor_dtype)
  * Returns the data type.
* [const TensorShape&amp; tensorflow::Tensor::shape](#const_TensorShape_amp_tensorflow_Tensor_shape)
  * Returns the shape of the tensor.
* [int tensorflow::Tensor::dims](#int_tensorflow_Tensor_dims)
  * Convenience accessor for the tensor shape.
* [int64 tensorflow::Tensor::dim_size](#int64_tensorflow_Tensor_dim_size)
  * Convenience accessor for the tensor shape.
* [int64 tensorflow::Tensor::NumElements](#int64_tensorflow_Tensor_NumElements)
  * Convenience accessor for the tensor shape.
* [bool tensorflow::Tensor::IsSameSize](#bool_tensorflow_Tensor_IsSameSize)
* [bool tensorflow::Tensor::IsInitialized](#bool_tensorflow_Tensor_IsInitialized)
  * Has this Tensor been initialized?
* [size_t tensorflow::Tensor::TotalBytes](#size_t_tensorflow_Tensor_TotalBytes)
  * Returns the estimated memory usage of this tensor.
* [Tensor&amp; tensorflow::Tensor::operator=](#Tensor_amp_tensorflow_Tensor_operator_)
  * Assign operator. This tensor shares other&apos;s underlying storage.
* [bool tensorflow::Tensor::CopyFrom](#bool_tensorflow_Tensor_CopyFrom)
  * Copy the other tensor into this tensor and reshape it.
* [Tensor tensorflow::Tensor::Slice](#Tensor_tensorflow_Tensor_Slice)
  * Slice this tensor along the 1st dimension.
* [bool tensorflow::Tensor::FromProto](#bool_tensorflow_Tensor_FromProto)
  * Parse "other&apos; and construct the tensor.
* [bool tensorflow::Tensor::FromProto](#bool_tensorflow_Tensor_FromProto)
* [void tensorflow::Tensor::AsProtoField](#void_tensorflow_Tensor_AsProtoField)
  * Fills in &quot;proto&quot; with &quot;*this&quot; tensor&apos;s content.
* [void tensorflow::Tensor::AsProtoTensorContent](#void_tensorflow_Tensor_AsProtoTensorContent)
* [TTypes&lt;T&gt;::Vec tensorflow::Tensor::vec](#TTypes_lt_T_gt_Vec_tensorflow_Tensor_vec)
  * Return the Tensor data as an Eigen::Tensor with the type and sizes of this Tensor .
* [TTypes&lt;T&gt;::Matrix tensorflow::Tensor::matrix](#TTypes_lt_T_gt_Matrix_tensorflow_Tensor_matrix)
* [TTypes&lt; T, NDIMS &gt;::Tensor tensorflow::Tensor::tensor](#TTypes_lt_T_NDIMS_gt_Tensor_tensorflow_Tensor_tensor)
* [TTypes&lt;T&gt;::Flat tensorflow::Tensor::flat](#TTypes_lt_T_gt_Flat_tensorflow_Tensor_flat)
  * Return the Tensor data as an Eigen::Tensor of the data type and a specified shape.
* [TTypes&lt;T&gt;::UnalignedFlat tensorflow::Tensor::unaligned_flat](#TTypes_lt_T_gt_UnalignedFlat_tensorflow_Tensor_unaligned_flat)
* [TTypes&lt;T&gt;::Matrix tensorflow::Tensor::flat_inner_dims](#TTypes_lt_T_gt_Matrix_tensorflow_Tensor_flat_inner_dims)
* [TTypes&lt;T&gt;::Matrix tensorflow::Tensor::flat_outer_dims](#TTypes_lt_T_gt_Matrix_tensorflow_Tensor_flat_outer_dims)
* [TTypes&lt; T, NDIMS &gt;::Tensor tensorflow::Tensor::shaped](#TTypes_lt_T_NDIMS_gt_Tensor_tensorflow_Tensor_shaped)
* [TTypes&lt; T, NDIMS &gt;::UnalignedTensor tensorflow::Tensor::unaligned_shaped](#TTypes_lt_T_NDIMS_gt_UnalignedTensor_tensorflow_Tensor_unaligned_shaped)
* [TTypes&lt; T &gt;::Scalar tensorflow::Tensor::scalar](#TTypes_lt_T_gt_Scalar_tensorflow_Tensor_scalar)
  * Return the Tensor data as a Tensor Map of fixed size 1: TensorMap&lt;TensorFixedSize&lt;T, 1&gt;&gt;.
* [TTypes&lt;T&gt;::ConstVec tensorflow::Tensor::vec](#TTypes_lt_T_gt_ConstVec_tensorflow_Tensor_vec)
  * Const versions of all the methods above.
* [TTypes&lt;T&gt;::ConstMatrix tensorflow::Tensor::matrix](#TTypes_lt_T_gt_ConstMatrix_tensorflow_Tensor_matrix)
* [TTypes&lt; T, NDIMS &gt;::ConstTensor tensorflow::Tensor::tensor](#TTypes_lt_T_NDIMS_gt_ConstTensor_tensorflow_Tensor_tensor)
* [TTypes&lt;T&gt;::ConstFlat tensorflow::Tensor::flat](#TTypes_lt_T_gt_ConstFlat_tensorflow_Tensor_flat)
* [TTypes&lt;T&gt;::ConstUnalignedFlat tensorflow::Tensor::unaligned_flat](#TTypes_lt_T_gt_ConstUnalignedFlat_tensorflow_Tensor_unaligned_flat)
* [TTypes&lt;T&gt;::ConstMatrix tensorflow::Tensor::flat_inner_dims](#TTypes_lt_T_gt_ConstMatrix_tensorflow_Tensor_flat_inner_dims)
* [TTypes&lt;T&gt;::ConstMatrix tensorflow::Tensor::flat_outer_dims](#TTypes_lt_T_gt_ConstMatrix_tensorflow_Tensor_flat_outer_dims)
* [TTypes&lt; T, NDIMS &gt;::ConstTensor tensorflow::Tensor::shaped](#TTypes_lt_T_NDIMS_gt_ConstTensor_tensorflow_Tensor_shaped)
* [TTypes&lt; T, NDIMS &gt;::ConstUnalignedTensor tensorflow::Tensor::unaligned_shaped](#TTypes_lt_T_NDIMS_gt_ConstUnalignedTensor_tensorflow_Tensor_unaligned_shaped)
* [TTypes&lt; T &gt;::ConstScalar tensorflow::Tensor::scalar](#TTypes_lt_T_gt_ConstScalar_tensorflow_Tensor_scalar)
* [string tensorflow::Tensor::SummarizeValue](#string_tensorflow_Tensor_SummarizeValue)
  * Render the first max_entries values in *this into a string.
* [string tensorflow::Tensor::DebugString](#string_tensorflow_Tensor_DebugString)
  * A human-readable summary of the Tensor suitable for debugging.
* [void tensorflow::Tensor::FillDescription](#void_tensorflow_Tensor_FillDescription)
* [StringPiece tensorflow::Tensor::tensor_data](#StringPiece_tensorflow_Tensor_tensor_data)
  * Returns a StringPiece mapping the current tensor&apos;s buffer.

##Member Details

#### tensorflow::Tensor::Tensor() {#tensorflow_Tensor_Tensor}

Default Tensor constructor. Creates a 1-dimension, 0-element float tensor.



#### tensorflow::Tensor::Tensor(DataType type, const TensorShape &amp;shape) {#tensorflow_Tensor_Tensor}

Creates a Tensor of the given datatype and shape.

The underlying buffer is allocated using a CPUAllocator.

#### tensorflow::Tensor::Tensor(Allocator *a, DataType type, const TensorShape &amp;shape) {#tensorflow_Tensor_Tensor}

Creates a tensor with the input datatype and shape, using the allocator &apos;a&apos; to allocate the underlying buffer.

&apos;a&apos; must outlive the lifetime of this Tensor .

#### tensorflow::Tensor::Tensor(DataType type) {#tensorflow_Tensor_Tensor}

Creates an uninitialized Tensor of the given data type.



#### tensorflow::Tensor::Tensor(const Tensor &amp;other) {#tensorflow_Tensor_Tensor}





#### tensorflow::Tensor::~Tensor() {#tensorflow_Tensor_Tensor}

Copy constructor.



#### DataType tensorflow::Tensor::dtype() const {#DataType_tensorflow_Tensor_dtype}

Returns the data type.



#### const TensorShape&amp; tensorflow::Tensor::shape() const {#const_TensorShape_amp_tensorflow_Tensor_shape}

Returns the shape of the tensor.



#### int tensorflow::Tensor::dims() const {#int_tensorflow_Tensor_dims}

Convenience accessor for the tensor shape.

For all shape accessors, see comments for relevant methods of TensorShape in tensor_shape.h .

#### int64 tensorflow::Tensor::dim_size(int d) const {#int64_tensorflow_Tensor_dim_size}

Convenience accessor for the tensor shape.



#### int64 tensorflow::Tensor::NumElements() const {#int64_tensorflow_Tensor_NumElements}

Convenience accessor for the tensor shape.



#### bool tensorflow::Tensor::IsSameSize(const Tensor &amp;b) const {#bool_tensorflow_Tensor_IsSameSize}





#### bool tensorflow::Tensor::IsInitialized() const {#bool_tensorflow_Tensor_IsInitialized}

Has this Tensor been initialized?



#### size_t tensorflow::Tensor::TotalBytes() const {#size_t_tensorflow_Tensor_TotalBytes}

Returns the estimated memory usage of this tensor.



#### Tensor&amp; tensorflow::Tensor::operator=(const Tensor &amp;other) {#Tensor_amp_tensorflow_Tensor_operator_}

Assign operator. This tensor shares other&apos;s underlying storage.



#### bool tensorflow::Tensor::CopyFrom(const Tensor &amp;other, const TensorShape &amp;shape) TF_MUST_USE_RESULT {#bool_tensorflow_Tensor_CopyFrom}

Copy the other tensor into this tensor and reshape it.

This tensor shares other&apos;s underlying storage. Returns true iff other.shape() has the same number of elements of the given &quot;shape&quot;.

#### Tensor tensorflow::Tensor::Slice(int64 dim0_start, int64 dim0_limit) const {#Tensor_tensorflow_Tensor_Slice}

Slice this tensor along the 1st dimension.

I.e., the returned tensor satisifies returned[i, ...] == this[dim0_start + i, ...]. The returned tensor shares the underlying tensor buffer with this tensor.

NOTE: The returned tensor may not satisfies the same alignment requirement as this tensor depending on the shape. The caller must check the returned tensor&apos;s alignment before calling certain methods that have alignment requirement (e.g., flat() , tensor()).

REQUIRES: dims() &gt;= 1 REQUIRES: 0 &lt;= dim0_start &lt;= dim0_limit &lt;= dim_size(0)

#### bool tensorflow::Tensor::FromProto(const TensorProto &amp;other) TF_MUST_USE_RESULT {#bool_tensorflow_Tensor_FromProto}

Parse "other&apos; and construct the tensor.

Returns true iff the parsing succeeds. If the parsing fails, the state of &quot;*this&quot; is unchanged.

#### bool tensorflow::Tensor::FromProto(Allocator *a, const TensorProto &amp;other) TF_MUST_USE_RESULT {#bool_tensorflow_Tensor_FromProto}





#### void tensorflow::Tensor::AsProtoField(TensorProto *proto) const {#void_tensorflow_Tensor_AsProtoField}

Fills in &quot;proto&quot; with &quot;*this&quot; tensor&apos;s content.

AsProtoField() fills in the repeated field for proto.dtype(), while AsProtoTensorContent() encodes the content in proto.tensor_content() in a compact form.

#### void tensorflow::Tensor::AsProtoTensorContent(TensorProto *proto) const {#void_tensorflow_Tensor_AsProtoTensorContent}





#### TTypes&lt;T&gt;::Vec tensorflow::Tensor::vec() {#TTypes_lt_T_gt_Vec_tensorflow_Tensor_vec}

Return the Tensor data as an Eigen::Tensor with the type and sizes of this Tensor .

Use these methods when you know the data type and the number of dimensions of the Tensor and you want an Eigen::Tensor automatically sized to the Tensor sizes. The implementation check fails if either type or sizes mismatch.

Example: typedef float T; Tensor my_mat(...built with Shape{rows: 3, cols: 5}...); auto mat = my_mat.matrix&lt;T&gt;(); // 2D Eigen::Tensor, 3 x 5. auto mat = my_mat.tensor&lt;T, 2&gt;(); // 2D Eigen::Tensor, 3 x 5. auto vec = my_mat.vec&lt;T&gt;(); // CHECK fails as my_mat is 2D. auto vec = my_mat.tensor&lt;T, 3&gt;(); // CHECK fails as my_mat is 2D. auto mat = my_mat.matrix&lt;int32&gt;();// CHECK fails as type mismatch.

#### TTypes&lt;T&gt;::Matrix tensorflow::Tensor::matrix() {#TTypes_lt_T_gt_Matrix_tensorflow_Tensor_matrix}





#### TTypes&lt; T, NDIMS &gt;::Tensor tensorflow::Tensor::tensor() {#TTypes_lt_T_NDIMS_gt_Tensor_tensorflow_Tensor_tensor}





#### TTypes&lt;T&gt;::Flat tensorflow::Tensor::flat() {#TTypes_lt_T_gt_Flat_tensorflow_Tensor_flat}

Return the Tensor data as an Eigen::Tensor of the data type and a specified shape.

These methods allow you to access the data with the dimensions and sizes of your choice. You do not need to know the number of dimensions of the Tensor to call them. However, they CHECK that the type matches and the dimensions requested creates an Eigen::Tensor with the same number of elements as the Tensor .

Example: typedef float T; Tensor my_ten(...built with Shape{planes: 4, rows: 3, cols: 5}...); // 1D Eigen::Tensor, size 60: auto flat = my_ten.flat&lt;T&gt;(); // 2D Eigen::Tensor 12 x 5: auto inner = my_ten.flat_inner_dims&lt;T&gt;(); // 2D Eigen::Tensor 4 x 15: auto outer = my_ten.shaped&lt;T, 2&gt;({4, 15}); // CHECK fails, bad num elements: auto outer = my_ten.shaped&lt;T, 2&gt;({4, 8}); // 3D Eigen::Tensor 6 x 5 x 2: auto weird = my_ten.shaped&lt;T, 3&gt;({6, 5, 2}); // CHECK fails, type mismatch: auto bad = my_ten.flat&lt;int32&gt;();

#### TTypes&lt;T&gt;::UnalignedFlat tensorflow::Tensor::unaligned_flat() {#TTypes_lt_T_gt_UnalignedFlat_tensorflow_Tensor_unaligned_flat}





#### TTypes&lt;T&gt;::Matrix tensorflow::Tensor::flat_inner_dims() {#TTypes_lt_T_gt_Matrix_tensorflow_Tensor_flat_inner_dims}



Returns the data as an Eigen::Tensor with 2 dimensions, collapsing all Tensor dimensions but the last one into the first dimension of the result.

#### TTypes&lt;T&gt;::Matrix tensorflow::Tensor::flat_outer_dims() {#TTypes_lt_T_gt_Matrix_tensorflow_Tensor_flat_outer_dims}



Returns the data as an Eigen::Tensor with 2 dimensions, collapsing all Tensor dimensions but the first one into the last dimension of the result.

#### TTypes&lt; T, NDIMS &gt;::Tensor tensorflow::Tensor::shaped(gtl::ArraySlice&lt; int64 &gt; new_sizes) {#TTypes_lt_T_NDIMS_gt_Tensor_tensorflow_Tensor_shaped}





#### TTypes&lt; T, NDIMS &gt;::UnalignedTensor tensorflow::Tensor::unaligned_shaped(gtl::ArraySlice&lt; int64 &gt; new_sizes) {#TTypes_lt_T_NDIMS_gt_UnalignedTensor_tensorflow_Tensor_unaligned_shaped}





#### TTypes&lt; T &gt;::Scalar tensorflow::Tensor::scalar() {#TTypes_lt_T_gt_Scalar_tensorflow_Tensor_scalar}

Return the Tensor data as a Tensor Map of fixed size 1: TensorMap&lt;TensorFixedSize&lt;T, 1&gt;&gt;.

Using scalar() allows the compiler to perform optimizations as the size of the tensor is known at compile time.

#### TTypes&lt;T&gt;::ConstVec tensorflow::Tensor::vec() const {#TTypes_lt_T_gt_ConstVec_tensorflow_Tensor_vec}

Const versions of all the methods above.



#### TTypes&lt;T&gt;::ConstMatrix tensorflow::Tensor::matrix() const {#TTypes_lt_T_gt_ConstMatrix_tensorflow_Tensor_matrix}





#### TTypes&lt; T, NDIMS &gt;::ConstTensor tensorflow::Tensor::tensor() const {#TTypes_lt_T_NDIMS_gt_ConstTensor_tensorflow_Tensor_tensor}





#### TTypes&lt;T&gt;::ConstFlat tensorflow::Tensor::flat() const {#TTypes_lt_T_gt_ConstFlat_tensorflow_Tensor_flat}





#### TTypes&lt;T&gt;::ConstUnalignedFlat tensorflow::Tensor::unaligned_flat() const {#TTypes_lt_T_gt_ConstUnalignedFlat_tensorflow_Tensor_unaligned_flat}





#### TTypes&lt;T&gt;::ConstMatrix tensorflow::Tensor::flat_inner_dims() const {#TTypes_lt_T_gt_ConstMatrix_tensorflow_Tensor_flat_inner_dims}





#### TTypes&lt;T&gt;::ConstMatrix tensorflow::Tensor::flat_outer_dims() const {#TTypes_lt_T_gt_ConstMatrix_tensorflow_Tensor_flat_outer_dims}





#### TTypes&lt; T, NDIMS &gt;::ConstTensor tensorflow::Tensor::shaped(gtl::ArraySlice&lt; int64 &gt; new_sizes) const {#TTypes_lt_T_NDIMS_gt_ConstTensor_tensorflow_Tensor_shaped}





#### TTypes&lt; T, NDIMS &gt;::ConstUnalignedTensor tensorflow::Tensor::unaligned_shaped(gtl::ArraySlice&lt; int64 &gt; new_sizes) const {#TTypes_lt_T_NDIMS_gt_ConstUnalignedTensor_tensorflow_Tensor_unaligned_shaped}





#### TTypes&lt; T &gt;::ConstScalar tensorflow::Tensor::scalar() const {#TTypes_lt_T_gt_ConstScalar_tensorflow_Tensor_scalar}





#### string tensorflow::Tensor::SummarizeValue(int64 max_entries) const {#string_tensorflow_Tensor_SummarizeValue}

Render the first max_entries values in *this into a string.



#### string tensorflow::Tensor::DebugString() const {#string_tensorflow_Tensor_DebugString}

A human-readable summary of the Tensor suitable for debugging.



#### void tensorflow::Tensor::FillDescription(TensorDescription *description) const {#void_tensorflow_Tensor_FillDescription}



Fill in the TensorDescription proto with metadata about the Tensor that is useful for monitoring and debugging.

#### StringPiece tensorflow::Tensor::tensor_data() const {#StringPiece_tensorflow_Tensor_tensor_data}

Returns a StringPiece mapping the current tensor&apos;s buffer.

The returned StringPiece may point to memory location on devices that the CPU cannot address directly.

NOTE: The underlying Tensor buffer is refcounted, so the lifetime of the contents mapped by the StringPiece matches the lifetime of the buffer; callers should arrange to make sure the buffer does not get destroyed while the StringPiece is still used.

REQUIRES: DataTypeCanUseMemcpy( dtype() ).
