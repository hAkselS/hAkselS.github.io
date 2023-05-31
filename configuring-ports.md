# Constructing Ports 

## Setup 

Start by making a directory will the ports will be defined. In this tutorial, the directory will be named "Ports". 

```shell 
# In: MathProject
mkdir Ports 
cd Ports
```

While in "Ports", create an empty fpp file called MathPorts.fpp, this is where the ports will be defined.

```shell 
# In: Ports
touch MathPorts.fpp
```

## Implementing the Ports

Use your favorite text editor to add the following to MathPorts.fpp 

```
module MathModule{ 
  @ Port for requesting an operation on two numbers
  port MathOp(
    val1: F32 @< The first operand
    op: MathOp @< The operation
    val2: F32 @< The second operand
  )

  @ Port for returning the result of a math operation
  port MathResult(
    result: F32 @< the result of the operation
  )
}
```
Notice how we have used the MathModule again while defining the ports. Here we have created two ports. The first port, called MathOp, carries two 32-bit floats (val1 and val2) and a math operations (op). The second port only carries one 32-bit float (result). The first port is intended to send operands and an operation to the math receiver. The second port is designed to send the results of the operat ion back to the sender. 

## Adding to the Build 

Create a CMakeLists.txt file in Types. 

```shell 
# In: Types
touch CMakeLists.txt 
```

Add the following to the CMakeLists.txt. 

```cmake
set(SOURCE_FILES
  "${CMAKE_CURRENT_LIST_DIR}/MathPorts.fpp"
)

register_fprime_module()
```

Now modifiy add the following to project.cmake. Remember that project.cmake is in MathProject, not Ports. 

```cmake 
add_fprime_subdirectory("${CMAKE_CURRENT_LIST_DIR}/Ports/")
```

Ports should build without any issues. Use the following build.

```shell
# In: Ports
fprime-util build
```

