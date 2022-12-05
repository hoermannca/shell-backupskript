# shell-backupskript
#!/bin/bash

#
#
#

function menu (){
        echo "|-----------------------------------|"
        echo "| Hauptmenu :                       |"
        echo "|    Backup erstellen :      1      |"
        echo "|    Inhalt eines Backups :  2      |"
        echo "|    Backup zurück spielen : 3      |"
        echo "|                                   |"
        read -p "| Eingabe : " EINGABE
        echo "|                                   |"
        echo "|-----------------------------------|"
}




function backup(){
        echo "BACKUP"
}
function unbackup(){
        echo "UNBACKUP"
function listbackup(){
        echo "LISTBACKUP"
}

while :
do
        clear
        menu
        case $EINGABE in
                1)
                        backup
                        ;;
                2)      unbackup
                        ;;
                3)      listbackup
                        ;;
                *)
                        echo "UND Tschüss"
                        exit 0
        esac


        echo $EINGABE
        sleep 2

done

exit 1
