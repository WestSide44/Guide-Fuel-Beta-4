# Deploy smart contract 

- VPS

- Ubuntu 22.04
  
- RAM 2 GB (Anything less will crash when the contract is deployed)


## Server Preparation

## Upgrade packages and the system

  
  ```
  apt update 
  ```

![](https://i.imgur.com/FCnCxfi.png)
    
  
  
  ``` 
  apt upgrade
  ```

[![3.png](https://i.postimg.cc/mg7hmJQp/3.png)](https://postimg.cc/mP2bDdp7)


Press `y `

## install Git
  
 
  ```
sudo apt-get install git-all
  ```


Let's check the version 

  
   ```
 git version
  ```


## Install Rust Toolchain

 
  ```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
[![6.png](https://i.postimg.cc/P56fVHC4/6.png)](https://postimg.cc/5XCMjZqY)

Press `1`


## Configuring the Shell


```
source "$HOME/.cargo/env"
 ```

## Updating Rust

 
  ```
rustup update stable
  ```

 
  ```
rustup default stable
  ```

## install the Fuel toolchain


```
curl --proto '=https' --tlsv1.2 -sSf https://install.fuel.network/fuelup-init.sh | sh
```
[![7.png](https://i.postimg.cc/gc5vQ9ZG/7.png)](https://postimg.cc/PNWpvRy7)



Press `y`


## Configure PATH


```
export PATH="$HOME/.fuelup/bin:$PATH"
```


```
source /root/.bashrc
```


## Installs the toolchain


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
[![8.png](https://i.postimg.cc/s23zzDLS/8.png)](https://postimg.cc/v42kLMbH)


## Create a contract folder


```
mkdir fuel-project
```


```
cd fuel-project
```


## Contract creation


```
forc new counter-contract
```


You should get the following

[![9.png](https://i.postimg.cc/nhhzK2HN/9.png)](https://postimg.cc/pp3RRD5B)


The next step is to change the contract file, choose a method that is convenient for you:


- ## 1 Way

Go to the specified path `fuel-project/counter-contract/src/main.sw` and modify the contract file using any graphical application. I use **MobaXterm Professional**


- ## 2 Way
Open the file directly from the terminal


```
nano counter-contract/src/main.sw
 
```
[![10.png](https://i.postimg.cc/fb00XCCD/10.png)](https://postimg.cc/v1bBwWCN)


completely delete the contents of the file and 
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


- ## 3 way


### Install VIM 


```
sudo apt install vim
```


Go to the file


```
vim counter-contract/src/main.sw
```
[![11.png](https://i.postimg.cc/C1gHx9gW/11.png)](https://postimg.cc/d75TWHDB)


- `V` to enter visual line mode, i.e. selection mode

- `i` for `insert` this immediately switches vim to insert mode

delete the content and insert the contract address from the previous method or from the **[official manual](https://docs.fuel.network/guides/quickstart/building-a-smart-contract/#writing-a-sway-smart-contract)**


After the changes have been made, do the following:

- Press `Esc` key to escape from Insert more
- Type `:w` and press `Enter` to save changes
- Type `:q` to close the document


If you don't understand the controls in Vim mode, check out this **[short tutorial](https://www.freecodecamp.org/news/vim-editor-modes-explained/)**


go to the contract folder


```
cd counter-contract
```


## Build the contract


```
forc build
```

the result should be
[![12.png](https://i.postimg.cc/9f0QQ8x4/12.png)](https://postimg.cc/jWVb8XYK)


## Wallet setup


Import Existing Wallet 

You will need to import the seedphrase from your `Fuel Wallet` extension.  If you don't have the extension, install it from the [Chrome store](https://chromewebstore.google.com/detail/fuel-wallet/dldjpboieedgcmpkchcjcbijingjcgok?hl=ru&utm_source=ext_sidebar) 

Lets import our seedphrase


```
forc-wallet import
```

[![13.png](https://i.postimg.cc/GtPn84Hb/13.png)](https://postimg.cc/H8LhFswN)

copy your seedphrase and paste it into the command line and press `Enter` (after pasting your phrase will remain invisible for security reasons).

then you need to enter your desired password and press `Enter`

Re-enter the password

create an account with your imported seedphrase


```
forc wallet account new
```

[![14.png](https://i.postimg.cc/3Nz0Rb4s/14.png)](https://postimg.cc/K3r8pf5f)

Enter your wallet password 


[![15.png](https://i.postimg.cc/nzgqjLNS/15.png)](https://postimg.cc/mz3PKTL7)

and you should see your wallet address in the terminal


## Creating a new wallet in the terminal


```
forc wallet new
```

Enter the desired password 
Be sure to save the seedphrase from your wallet


## Create a wallet account


```
forc wallet account new
```

Getting tokens from the faucet
To deploy a smart contract you need some test tokens, go to **[faucet](https://faucet-beta-4.fuel.network/?address=fuel13hj0rj3r7443ka9dcv7g9mt89v7pdell2my60kdantx6jqq57yuqqsax06)** and insert your wallet and get tokens


or open the faucet directly from your wallet



[![image.png](https://i.postimg.cc/Bvv4DqdM/image.png)](https://postimg.cc/MngCJ8ZQ)




## Deploy smart contract


```
forc deploy --testnet
```


[![16.png](https://i.postimg.cc/V6J4JpZg/16.png)](https://postimg.cc/sQR586rG)



Re-enter the password


[![17.png](https://i.postimg.cc/K8mNPRsR/17.png)](https://postimg.cc/pp1zxXvH)


After entering your password, you need to enter your wallet index 
enter `0` and press `y`


Done


[![18.png](https://i.postimg.cc/nhwDXr88/18.png)](https://postimg.cc/pmzT72Xk)


check your transaction in [explorer](https://fuellabs.github.io/block-explorer-v2/beta-4/)


[![19.png](https://i.postimg.cc/05fr6jmt/19.png)](https://postimg.cc/WtdsC25r)


all right. You did it !

