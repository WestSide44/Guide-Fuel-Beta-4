## Deploy smart contract 

(VPS) 

Ubuntu 22.04
  
RAM 2 GB (Anything less will crash when the contract is deployed)


## Server Preparation

Upgrade packages and the system

  
  ```
  apt update 
  ```
    
  
  ``` 
  apt upgrade
  ```

install Git
  
  ```
sudo apt-get install git-all

  ```

Let's check the version 

   ```
 git version
  ```


Install Rust Toolchain

  ```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

  ```

Configuring the Shell

  ```
source "$HOME/.cargo/env"
 
 ```

Updating Rust

  ```
rustup update stable
  ```

  ```
rustup default stable
  ```

install the Fuel toolchain

```
curl --proto '=https' --tlsv1.2 -sSf https://install.fuel.network/fuelup-init.sh | sh
```

Configure PATH

```
export PATH="$HOME/.fuelup/bin:$PATH"
```

```
source /root/.bashrc
```

Installs the toolchain

```
fuelup toolchain install beta-4
```

```
fuelup default beta-4
```

Check the version

```
fuelup --version
```

create a contract folder

```
mkdir fuel-project
```

```
cd fuel-project
```

contract creation

```
forc new counter-contract
```

The next step is to change the contract file, choose a method that is convenient for you:

1 Way

Go to the specified path counter-contract/src/main.sw and modify the contract file using any graphical application. I use MobaXterm Professional.

2 Way 
Open the file directly from the terminal
nano counter-contract/src/main.sw , completely delete the contents of the file and 
insert the contract :

```
contract;
 
storage {
    counter: u64 = 0,
}
 
abi Counter {
    #[storage(read, write)]
    fn increment();
 
    #[storage(read)]
    fn count() -> u64;
}
 
impl Counter for Contract {
    #[storage(read)]
    fn count() -> u64 {
        storage.counter.read()
    }
 
    #[storage(read, write)]
    fn increment() {
        let incremented = storage.counter.read() + 1;
        storage.counter.write(incremented);
    }
}
```

3 way
Install VIM 

```
sudo apt install vim
```

Go to the file
```
vim counter-contract/src/main.sw
```

`V` to enter visual line mode, i.e. selection mode

`i` for `insert` this immediately switches vim to insert mode

delete the content and insert the contract address from the previous method or from the official manual

After the changes have been made, do the following:

Press `Esc` key to escape from Insert more
Type `:w` and press `Enter` to save changes
Type `:q` to close the document

go to the contract folder
```
cd counter-contract
```

build the contract

```
forc build
```

Wallet setup

1) Import Existing Wallet 

You will need to import the seedphrase from your `Fuel Wallet` extension.  If you don't have the extension, install it from the Chrome store

Lets import our seedphrase

```
forc-wallet import
```

copy your seedphrase and paste it into the command line and press `Enter` (after pasting your phrase will remain invisible for security reasons).

then you need to enter your desired password and press `Enter`

Re-enter the password

create an account with your imported seedphrase

```
forc wallet account new
```
Enter your wallet password 
and you should see your wallet address in the terminal

Creating a new wallet in the terminal

```
forc wallet new
```

Enter the desired password 
Be sure to save the seedphrase from your wallet

Create a wallet account

```
forc wallet account new
```

Getting tokens from the faucet
To deploy a smart contract you need some test tokens, go here ..... insert your wallet and get tokens

Deploy smart contract

```
forc deploy --testnet
```
Re-enter the password

After entering your password, you need to enter your wallet index 
enter `0` and press `y`

Done

check your transaction in explorer ....

all right. You did it !

