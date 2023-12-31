# Setting Up `local-bin` Repository

Welcome to the `local-bin` repository! This collection contains essential scripts for various use cases stored in the `local-bin` directory. Follow these simple steps to set up and integrate these scripts into your shell environment.

## Clone the Repository

Open your terminal and run the following command to clone the repository:

```bash
cd ~
git clone https://github.com/nikhilesh-gupta/local-bin
```

# Update Shell Configuration

## For BASH Users

If you are using the BASH shell, follow these steps to update your shell configuration:

1. Open your BASH configuration file:

    ```bash
    vim ~/.bashrc
    ```

2. Add the following line to update the PATH variable:

    ```bash
    export PATH=$PATH:$HOME/local-bin/
    ```

3. Save the file.

4. Update the BASH shell environment:

    ```bash
    source ~/.bashrc
    ```

## For ZSH Users

If you are using the ZSH shell, follow these steps to update your shell configuration:

1. Open your ZSH configuration file:

    ```bash
    vim ~/.zshrc
    ```

2. Add the following line to update the PATH variable:

    ```bash
    export PATH=$PATH:$HOME/local-bin/
    ```

3. Save the file.

4. Update the ZSH shell environment:

    ```bash
    source ~/.zshrc
    ```

Now you're all set! Your shell environment is configured to include the scripts from the `local-bin` repository.
