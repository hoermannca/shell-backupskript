#!/bin/bash

# Backup: Erstellen und Zurückspielen von Verzeichnissen
# Author : Calvin Hörmann
# E-Mail : hoermannca@elektronikschule.de
# Version: 1

# Hauptmenu ausgeben
function menu(){
	clear
	echo "|----------------------------------------------|"
	echo "| Haupmenu:                                    |"
	echo "|                                              |"
	echo "|      Backup erstellen:      B                |"
	echo "|      Inhalt eines Backups:  L                |"
	echo "|      Backup zurück spielen: R                |"
	echo "|      Backup löschen:        D                |"
	echo "|      Programm beenden:      X                |"
	echo "|                                              |"
	read -p "| Eingabe: " EINGABE
}


function compress(){
	clear
	echo "|----------------------------------------------|"
	echo "| Kompressionsmethode:                         |"
	echo "|                                              |"
	echo "|      ZIP:                   z                |"
	echo "|      BZIP2:                 j                |"
	echo "|      XZ:                    J                |"
	echo "|                                              |"
	read -p "| Eingabe: " COMPRESS
}
function where(){
	clear
	echo "|----------------------------------------------|"
	echo "| Wo soll nach dem Backup gesucht werden :    |"
	echo "|                                              |"
	read -p "| Eingabe: " WHERE
}
function typ(){
	clear
	echo "|----------------------------------------------|"
	echo "| Von welchem Datentyp soll das BAckup gesucht werden :    |"
	echo "|                                              |"
	read -p "| Eingabe: " TYP
}

function where2Backup(){
	clear
	echo "|----------------------------------------------|"
	echo "| Wohin soll das Backup gespeichert werden:    |"
	echo "|                                              |"
	read -p "| Eingabe: " WHERE2BACKUP
}


function what2Backup(){
	clear
	echo "|----------------------------------------------|"
	echo "| Was soll im Backup gespeichert werden:       |"
	echo "|                                              |"
	read -p "| Eingabe: " WHAT2BACKUP
}


function backup() {
    DATEINAME=$(date +%Y%m%d-%H%M%S)-backup.tgz
    YESNO=0
    until [ $YESNO = 1 ]
    do
        compress
        echo "| Sind Sie sich sicher,dass sie die Option $COMPRESS   |"
        echo "| benutzen möchten                                   |"
        read -p "| (0: nein |  1: ja) " YESNO
    done

    YESNO=0
    until [ $YESNO = 1 ]
    do
        where2Backup
        echo "| Sind Sie sich sicher,dass sie die Option $WHERE2BACKUP   |"
        echo "| benutzen möchten                                   |"
        read -p "| (0: nein |  1: ja) " YESNO
    done

    YESNO=0
    until [ $YESNO = 1 ]
    do
        what2Backup
        echo "| Sind Sie sich sicher,dass sie die Option $WHAT2BACKUP  |"
        echo "| benutzen möchten                                   |"
        read -p "| (0: nein |  1: ja) " YESNO
    done
    tar cf${COMPRESS} ${WHERE2BACKUP}/${DATEINAME} $WHAT2BACKUP

}

function unbackup(){
	echo "UNBACKUP"
}

function listbackup(){
	echo "LISTBACKUP"
}

function deletebackup(){
	echo "DELETEBACKUP"
	YESNO=0
    until [ $YESNO = 1 ]
    do
        where
        echo "| Sind Sie sich sicher,dass das Backup bei $WHERE    |"
        echo "| gesucht werden soll ?                                 |"
        read -p "| (0: nein |  1: ja) " YESNO
    done

    YESNO=0
    until [ $YESNO = 1 ]
    do
        typ
        echo "| Sind Sie sich sicher,dass das Backup den Datentyp $TYP   |"
        echo "| hat  ?                                 |"
        read -p "| (0: nein |  1: ja) " YESNO
    done

    echo " find $WHERE -name *.$TYP -typ -f "

}


while :
do
	menu
	case $EINGABE in
		b|B)
			backup
			;;
		r|R)
			unbackup
			;;
		l|L)
			listbackup
			;;
		d|D)
			deletebackup
			;;
		*)
			echo "Und Tschüss"
			exit 1
	esac
	sleep 2
done

exit 0
