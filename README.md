# MPI-Poisson-2D

## Description

This project is part of my Master's in Data Engineering (S2), specifically for the **Parallel Computing** module. It focuses on solving the **2D Poisson equation** using **MPI (Message Passing Interface)** with **Cartesian topologies** and the **Finite Difference Method (FDM)** to distribute computations efficiently across multiple processes.

## Table of Contents

- [Solution Overview](#solution-overview)
- [Mathematical Formulation](#mathematical-formulation)
- [Architecture](#architecture)  
  - [MPI Cartesian Grid](#mpi-cartesian-grid)  
  - [Communication Pattern](#communication-pattern)  
- [Installation and Configuration](#installation-and-configuration)  
  - [Prerequisites](#prerequisites)  
  - [Clone the Repository](#clone-the-repository)  
  - [Set Up a Virtual Environment and Install Dependencies](#set-up-a-virtual-environment-and-install-dependencies)  
  - [Example Execution](#example-execution)  
- [Usage](#usage)  
- [Results Visualization](#results-visualization)  
- [Contributing](#contributing)  
- [Contact Information](#contact-information)  


## Solution Overview

The project implements a **parallel solver** for the **2D Poisson equation** on a discretized grid using the **Finite Difference Method (FDM)**. The domain is decomposed into subdomains, which are distributed across multiple MPI processes using a **Cartesian topology** to efficiently handle inter-process communication.

![MPI Cartesian Grid](./solution_plot.png)


## Mathematical Formulation

The 2D Poisson equation is given by:

![alt text](formula.png)


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

- **Linux**
- **Python**
- **venv(Viratual Environment)**
- **Pip**

### Clone the Repository

```sh
git clone https://github.com/Starias22/MPI-Poisson-2D.git
cd MPI-Poisson-2D
```

### Set up a virtual environemnt and Install Pip dependences

```sh
python3 -m venv project_env
source project_env/bin/activate
pip install requirements.txt
```

### Example Execution

Example using **8 MPI processes**:

```sh
!mpiexec -n 8 python3 poisson.py 
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

## Contact Information

For questions or issues, please contact:

- **Name**: G. Ezéchiel ADEDE
- **Email**: [adedeezechiel@gmail.com](mailto\:adedeezechiel@gmail.com)
- **GitHub**: [Starias22](https://github.com/Starias22)
- **LinkedIn**: [G. Ezéchiel ADEDE](https://www.linkedin.com/in/Starias22)

