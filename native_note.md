More likely, I need native version

`coeffs = pywt.wavedec2(data=image_array, wavelet=self.__wavelet_func, level=5)` in https://github.com/PyWavelets/pywt/blob/1739712cca70ea4d47469e9279f5ea6b6c0770cd/pywt/_multilevel.py#L179

# Dependency
`AxisError` (from pywt/_utils.py)

`_wavelets_per_axis` (from pywt/_utils.py)
`_check_level` (from pywt/_multilevel.py)
    `dwt_max_level` (from pywt/_extensions/_dwt.py)
`dwt2` (from pywt/_multidim.py)
    `dwtn` (from pywt/_multidim.py)
        `dwt_axis` (from ._extensions._dwt)


The dwt_axis function in the _dwt.pyx file performs the discrete wavelet transform (DWT) along a specified axis of a multi-dimensional numpy array. Here's a step-by-step explanation of what it does:

1. Imports and Declarations:
    The function starts by importing necessary modules and declaring the variables to be used, including common.ArrayInfo, np.ndarray, and others.

2. Input Validations:
    It checks if the length of data along the specified axis is greater than 1 for MODE_REFLECT or MODE_ANTIREFLECT. If not, it raises a ValueError.

3. Data Type Check and Conversion:
    The input data is cast to an appropriate dtype using _check_dtype(data) to ensure compatibility.

4. Shape Calculations:
    It calculates the shapes of the input and output arrays. The output shape is updated along the specified axis to accommodate the wavelet coefficients.

5. Output Array Initialization:
    Two empty numpy arrays cA and cD are created to store the approximation and detail coefficients, respectively.

6. Data Info Initialization:
    It initializes data_info and output_info structures to hold information about the arrays, such as dimensions, strides, and shapes.

7. Wavelet Transform Execution:
    Depending on the data type (float64, float32, complex64, or complex128), it calls the corresponding C functions to perform the wavelet transform.
    The functions c_wt.double_downcoef_axis, c_wt.float_downcoef_axis, c_wt.float_complex_downcoef_axis, and c_wt.double_complex_downcoef_axis are used to compute the approximation (cA) and detail (cD) coefficients with no Python Global Interpreter Lock (GIL) to improve performance.

8. Error Handling:
    If the return value retval indicates an error, a RuntimeError is raised.

9. Return Coefficients:
    Finally, it returns the computed approximation (cA) and detail (cD) coefficients as a tuple.
