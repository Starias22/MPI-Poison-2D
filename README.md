# MPI-Poisson-2D

## Description

This project is part of my Master's in Data Engineering (S2), specifically for the **Parallel Computing** module. It focuses on solving the **2D Poisson equation** using **MPI (Message Passing Interface)** with **Cartesian topologies** and the **Finite Difference Method (FDM)** to distribute computations efficiently across multiple processes.

## Table of Contents

- [Solution Overview](#solution-overview)
- [Mathematical Formulation](#mathematical-formulation)
- [Architecture](#architecture)
  - [MPI Cartesian Grid](#mpi-cartesian-grid)
  - [Communication Pattern](#communication-pattern)
- [Installation and Configurations](#installation-and-configurations)
  - [Prerequisites](#prerequisites)
  - [Clone the Repository](#clone-the-repository)
  - [Build and Run the MPI Program](#build-and-run-the-mpi-program)
  - [Example Execution](#example-execution)
- [Usage](#usage)
- [Results Visualization](#results-visualization)
- [Contributing](#contributing)
- [License](#license)
- [Contact Information](#contact-information)

## Solution Overview

The project implements a **parallel solver** for the **2D Poisson equation** on a discretized grid using the **Finite Difference Method (FDM)**. The domain is decomposed into subdomains, which are distributed across multiple MPI processes using a **Cartesian topology** to efficiently handle inter-process communication.

## Mathematical Formulation

The 2D Poisson equation is given by:

\(\nabla^2 u = f(x, y)\)

where \(u(x, y)\) is the function to solve for, and \(f(x, y)\) is a known source term. The discretized version using the finite difference method is:

\(\frac{u_{i+1,j} - 2u_{i,j} + u_{i-1,j}}{\Delta x^2} + \frac{u_{i,j+1} - 2u_{i,j} + u_{i,j-1}}{\Delta y^2} = f_{i,j}\)

This results in a system of linear equations solved iteratively using **Jacobi, Gauss-Seidel, or Successive Over-Relaxation (SOR) methods**.

## Architecture

### MPI Cartesian Grid

MPI processes are arranged in a **2D Cartesian grid**, where each process is responsible for a subdomain of the full computational grid. Ghost cells are used to exchange boundary values between neighboring processes.

### Communication Pattern

- **Neighbor Exchange**: Each process communicates with its **top, bottom, left, and right** neighbors to share boundary values.
- **MPI\_Send/MPI\_Recv**: Used for explicit point-to-point communication.
- **MPI\_Cart\_create**: Creates a Cartesian communicator for efficient topology-aware communication.
- **MPI\_Cart\_shift**: Determines neighboring ranks for structured communication.

## Installation and Configurations

### Prerequisites

- **Linux** or **WSL (Windows Subsystem for Linux)**
- **MPI Implementation** (OpenMPI or MPICH)
- **Python (optional for visualization)**

### Clone the Repository

```sh
git clone https://github.com/Starias22/MPI-Poisson-2D.git
cd MPI-Poisson-2D
```

### Build and Run the MPI Program

Compile the MPI program using:

```sh
mpicc -o poisson_solver poisson.c -lm
```

Run the solver on multiple processes:

```sh
mpirun -np 4 ./poisson_solver
```

### Example Execution

Example with a **16x16 grid** using **4 MPI processes**:

```sh
mpirun -np 4 ./poisson_solver 16 16
```

## Usage

- Adjust **grid size** and **number of processes** in the execution command.
- Modify **source term** \(f(x, y)\) in the code for different Poisson problem scenarios.
- Choose different iterative **solvers** (Jacobi, Gauss-Seidel, etc.).

## Results Visualization

After execution, the plot can be seen  [here](./solution_plot.png)

## Contributing

We welcome contributions! Follow these steps:

1. Fork the repository.
2. Create a new branch: `git checkout -b feature-name`.
3. Commit changes: `git commit -m 'Add new feature'`.
4. Push to the branch: `git push origin feature-name`.
5. Submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact Information

For questions or issues, please contact:

- **Name**: G. Ezéchiel ADEDE
- **Email**: [adedeezechiel@gmail.com](mailto\:adedeezechiel@gmail.com)
- **GitHub**: [Starias22](https://github.com/Starias22)
- **LinkedIn**: [Gbètoho Ezéchiel ADEDE](https://www.linkedin.com/in/Starias22)

