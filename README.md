# Eigensolver Project

This project provides an implementation of an automatized eigensolver to compute eigenvalues and eigenfunctions for general one-body potentials. The solver can process various potential types and plot results using included Python scripts.


## Table of Contents
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
    - [Building the Project](#building-the-project)
    - [Running the Solver](#running-the-solver)
    - [Plotting Results](#plotting-results)
- [Project Structure](#project-structure)
- [Additional Notes](#additional-notes)

## Features
- Solves the eigenvalue problem for one-body Schrödinger equations.
- Supports multiple potential types (e.g. harmonic oscillator, Gaussian, Exponential, Double-well, Modified Morse)
- Visualizes results using Python plotting scripts.
- Modular structure for easy extension and maintenance.

## Requirements
- **Libraries:**
    - [MADNESS](https://github.com/m-a-d-n-e-s-s/madness): A prerequisite library for numerical computations.
    - (As of November 22, 2024) The option DENABLE_MPI=Off does not work with the current version of the MADNESS library.
    - To ensure the project works correctly, install the MADNESS library with MPI enabled. If MPI is not installed on your system, you can install it as follows:
        - Ubuntu: 

        ```bash
        sudo apt install openmpi-bin libopenmpi-dev
        ```
        - MacOS:

        ```bash
        brew install open-mpi
        ```
- **Python Packages:**
    - The following Python packages are required to run the plotting scripts:
        - Numpy
        - Matplotlib (version 3.7.1)
        - Tikzplotlib
        - natsort
        - webcolors (version 1.12)

## Installation
Before building the project, change the MADNESS library path in the `CMakeLists.txt` file to the correct path on your system. The MADNESS library path is defined in the `MADNESS_DIR` variable.

1. Clone the repository:

    ```bash
    git clone https://git.rz.uni-augsburg.de/qalg-a/automatized_eigensolver.git
    ```
2. Build the project:

    ```bash
    mkdir build_eigensolver
    cd build_eigensolver
    cmake ../automatized_eigensolver
    make
    ```
3. To run the eigensolver, execute the shell script `run_eigensolver.sh`:

    ```bash
    ./run_eigensolver.sh
    ```

## Usage
To create a GIF of the eigenfunctions for a specific potential type, make sure that your files are organized in the following structure:

```
|-- build_eigensolver/
|   |-- run_eigensolver.sh
|   |-- Images/               
|   |   |-- Gaussian/
|   |   |   |-- Potential.dat
|   |   |   |-- Gaussian_Phi/
|   |   |   |   |-- Phi_0/
|   |   |   |   |   |-- phi-0-0.dat
|   |   |   |   |   |-- phi-0-1.dat
|   |   |   |   |   |-- ...
|   |   |   |   |-- Phi_1/
|   |   |   |   |   |-- phi-1-0.dat
|   |   |   |   |   |-- phi-1-1.dat
|   |   |   |   |   |-- ...
|   |   |-- Gaussian_Psi/
|   |   |   |-- Psi_0.dat
|   |   |   |-- Psi_1.dat
|   |   |   |-- ...
```
### File Organization
- Put the `phi-*.dat` files in the corresponding `Phi_*` folders (located inside the folder for each potential type, e.g., `Gaussian_Phi`).
- Put the `Psi_*.dat` files in the `NAME_Psi` folder (e.g., Gaussian_Psi).

### Plotting the Results
1. To create the .png files for the eigenfunctions, run the `run_plot_phi.sh` script with the path to the `Phi` folder as an argument. For example:

    ```bash
    ./run_plot_phi.sh Images/Gaussian/Gaussian_Phi/
    ```
    
    This command will generate a `.png` file for each `.dat` file.
    
2. After the .png files are created, you can generate a GIF by running the Python script `togif.py`:

    ```bash
    ./togif.py Images/Gaussian/Gaussian_Phi/
    ```

## Project Structure
The project is organized as follows:

```
|-- automatized_eigensolver/
|   |-- Eigensolver/
|   |   |-- include/                <-- Header files for the eigensolver module
|   |   |   |-- ...
|   |   |-- src/                    <-- Source files for the eigensolver module
|   |   |   |-- eigensolver.cc      <-- Main implementation of the eigensolver
|   |   |-- plot/                   <-- Contains Python scripts for plotting results
|   |   |   |-- ...
|   |-- CMakeLists.txt              <-- CMake build configuration file
|-- build_eigensolver/              <-- Build directory
|   |-- run_eigensolver.sh          <-- Shell script to run the eigensolver
|   |-- Images/                     <-- Output folder for images and GIFs
|   |   |-- Gaussian/               <-- Folder for Gaussian potential type
|   |   |   |-- Potential.dat       <-- Potential data for Gaussian potential
|   |   |   |-- Gaussian_Phi/       <-- Folder for eigenfunction files (Phi)
|   |   |   |   |-- Phi_0/          <-- Folder for Phi_0 eigenfunctions
|   |   |   |   |   |-- phi-0-0.dat 
|   |   |   |   |   |-- phi-0-1.dat 
|   |   |   |   |-- Phi_1/          <-- Folder for Phi_1 eigenfunctions
|   |   |   |   |   |-- phi-1-0.dat 
|   |   |   |   |   |-- phi-1-1.dat 
|   |   |   |-- Gaussian_Psi/       <-- Folder for wavefunction files (Psi)
|   |   |   |   |-- Psi_0.dat       
|   |   |   |   |-- Psi_1.dat       
|   |   |   |   |-- ...
```

### Explanation of Folders and Files
- **automatized_eigensolver/**: Project root directory.
    - **Eigensolver/**: Contains source code and header files for the eigensolver module.
        - **include/**: Header files used for the eigensolver.
        - **src/**: Source files implementing the eigensolver.
        - **plot/**: Python scripts for visualizing results.
    - **CMakeLists.txt**: Build configuration file for CMake to compile the project.
- **build_eigensolver/**: The build directory where compiled files and results will be stored.
    - **run_eigensolver.sh**: Shell script to run the eigensolver.

Needed to be created manually in the build directory:
- **Images/**: Folder where output images (e.g., .png) and GIFs will be saved.
- **Gaussian/**: Example folder for the Gaussian potential type, showing the expected file structure.
- Note: Other potential types (e.g., Exponential, Double-well) should have similar folder structures within Images/.

### Additional Notes
If you have any questions or need further assistance with the project, feel free to reach out. I'm happy to help!
