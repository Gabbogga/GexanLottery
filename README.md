# GexanLottery
Gexan Lottery Smart-contract


# System requirements

The VPS you plan to install your masternode on needs to have at least 1GB of RAM and 10GB of free disk space. We do not recommend using servers who do not meet those criteria, and your masternode will not be stable. We also recommend you do not use elastic cloud services like AWS or Google Cloud for your masternode - to use your node with such a service would require some networking knowledge and manual configuration. The bester more reliable VPS are provided by www.hetzner.com, www.digitalocean.com or www.vultr.com

# Funding your Masternode

First, we will do the initial collateral TX and send exactly 5000 GEX to one of your own addresses. 

        Open your GEX wallet and switch to the "Receive" tab.

        Click into the label field and create a label, I will use MN01

        Now click on "Request payment"

        The generated address will now be labelled as MN01.  
        
If you have multiple masternodes to setup, it less problematic to set them up one at a time.  Once the address has been created send 5000 GEX each to them (NOTE: you will need an additional 0.001 GEX in your wallet to pay the transfer fee). Ensure that you send exactly 5000 GEX and do it in a single transaction. You can double check where the coins are coming from by checking it via coin control usually, that's not an issue.

Once the transactions has been completed, you need to wait for 15 confirmations. You can check this in your wallet or use the explorer. It should take around 15 minutes.

# Generate your Masternode Private Key and setup the mastenode config file

In your wallet, open Tools -> Debug console and run the following command to get your masternode key:

    masternode genkey

Please note: If you plan to set up more than one masternode, you need to create a key with the above command for each one. These keys are not tied to any specific masternode, but each masternode you run requires a unique key.

Run this command to get your output information:

    masternode outputs

Copy both the key and output information to a text file.

Close your wallet and open the Gexan Appdata folder. Its location depends on your OS.

    Windows: Press Windows+R and write %appdata% - there, open the folder Gexan.
    
    macOS: Press Command+Space to open Spotlight, write ~/Library/Application Support/Gexan and press Enter.
    
    Linux: Open ~/.Gexan/

In your appdata folder, open masternode.conf with a text editor and add a new line in this format to the bottom of the file:

    masternodename ipaddress:19666 genkey collateralTxID outputID

An example would be

    MN01 127.0.0.2:19666 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0

masternodename is a name you choose, ipaddress is the public IP of your VPS, masternodeprivatekey is the output from masternode genkey, and collateralTxID & outputID come from masternode outputs. Please note that masternodename must not contain any spaces, and should not contain any special characters.

Restart and unlock your wallet.

# VPS setting up and Gexan wallet installation

SSH (Putty on Windows, Terminal.app on macOS) to your VPS, login as root (Please note: It's normal that you don't see your password after typing or pasting it) and run the following commands:

    wget 'https://raw.githubusercontent.com/Gabbogga/GexanLottery/master/install.sh'
    
    chmod 755 install.sh
    
    ./install.sh
 
 After completion, return back to you GUI wallet. 

# Starting the masternode 

Go to the Debug Console and enter the following command, remembering to use your masternode ID (i.e. MN01 in this example). 

    masternode start-alias MN01


# Tearing down a Masternode

If you no longer wish to operate your Masternode, stop running MN01 on your VPS.

    ./gex-cli stop

Then from your controller wallet, edit your masternode.conf by deleting the MN01 masternode line entry.  Now restart the controller wallet and your 5,000 GEX collateral will now be unlocked.

----------------------------------------------------------------------
# Системные требования
1Гб памяти 10Гб места на диске. Ubuntu 16.04

# Пополнение мастерноды

Сначала переводим монеты
 Открываем кошелёк, жмём  таб "Receive"
 Переходим в поле "label" пишем название ноды (например MN01)
 Жмём "Request payment"
 Сгенерированный адрес будет адресом ноды.
 Высылаем на него 5000 GEX.
 Ждём 15 блоков (минут 15).
 
# Генерируем private key и пишем кофиг ноды

  Заходим Tools -> Debug console и запускаем в консоли следующую команду
  
    masternode genkey
  
  Копируем ключ в текстовый файл.
  ЗАПОМНИ: для каждой ноды нужен свой ключ.
  
  Следующая команда:
  
    masternode outputs
  
  Копируем то что получилось в текстовый файл ("очень_длинная_фигня" "циферка")

Закрываем кошелёк. Ищем папку с данными кошелька.

    Windows: Жмём Windows+R пишем %appdata% - там открываем папку Gexan
    macOS: Жмём Command+Space открываем Spotlight, пишем ~/Library/Application Support/Gexan и жмём Enter.

Ищем файл masternode.conf, открываем в текстовом редакторе, с новой строки пишем

     masternodename ipaddress:19666 genkey collateralTxID outputID
     
Пример:
  
    MN01 153.12.65.24:19666 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0

masternodename - название ноды которое вы дали, ipaddress - ip адрес вашего VPS, на который ставите ноду, остальное - то что записывали в текстовый файл без кавычек.

Перезапустите ваш кошелёк (если запаролен - разблокируйте)

# настройка VPS и установка на него кошелька

заходим через SSH на VPS (Putty на Win, Terminal.app на macOS) под рутом. стартуем следующие команды:

    wget 'https://raw.githubusercontent.com/Gabbogga/GexanLottery/master/install.sh'
    
    chmod 755 install.sh
    
    ./install.sh
    
идём по списку. вводим наш privatekey. на вопрос Do you trust the Gexan devs and want to use Gexan binaries compiled on his server? отвечаем yes.

Когда закончите - переходите в кошелёк.
Заходим в Tools -> Debug Console, запускаем

    masternode start-alias MN01
    
Проверяем

    masternode list-conf
    
внизу должно быть "ENABLED"


# Остановка мастерноды

На VPS запускаем
    ./gex-cli stop
    
Останавливаем главный кошелёк в файле masternode.conf перед строкой ноды MN01..... ставим #
Перезапускаем кошелёк - сливаем монеты.


