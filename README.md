import csv
import os
from colorama import init, Fore, Style


init(autoreset=True)


ascii_art = r'''
   _____                      __
  / ___/___  ____ ___________/ /_
  \__ \/ _ \/ __ `/ ___/ ___/ __ \
 ___/ /  __/ /_/ / /  / /__/ / / /
/____/\___/\____/_/   \___/_/ /_/

        D B   S E A R C H E R
'''


def search_in_csv(file_path, search_string):
    try:
        with open(file_path, mode='r', encoding='utf-8') as file:
            csv_reader = csv.reader(file)
            for row in csv_reader:
                if search_string in row:
                    print(Fore.GREEN + "String found in row:" + Style.RESET_ALL, row)
    except FileNotFoundError:
        print(Fore.RED + f"File not found: {file_path}" + Style.RESET_ALL)
    except Exception as e:
        print(Fore.RED + f"An error occurred: {e}" + Style.RESET_ALL)


def search_in_txt(file_path, search_string):
    try:
        with open(file_path, mode='r', encoding='utf-8') as file:
            for line_number, line in enumerate(file, start=1):
                if search_string in line:
                    print(Fore.GREEN + f"String found in line {line_number}:" + Style.RESET_ALL, line.strip())
    except FileNotFoundError:
        print(Fore.RED + f"File not found: {file_path}" + Style.RESET_ALL)
    except Exception as e:
        print(Fore.RED + f"An error occurred: {e}" + Style.RESET_ALL)

def main():
    print(Fore.CYAN + ascii_art + Style.RESET_ALL)
    print(Fore.MAGENTA + "By 501, this tool is strictly for legal and authorized use only." + Style.RESET_ALL)
    print(Fore.YELLOW + "DB Searcher Tool" + Style.RESET_ALL)
    print(Fore.CYAN + "-----------------" + Style.RESET_ALL)
    print("Instructions:")
    print("1. Provide the path to your CSV or TXT file.")
    print("2. Enter the string you want to search for.")
    print()

    
    file_path = input(Fore.CYAN + "Enter the path to your file: " + Style.RESET_ALL).strip()
    search_string = input(Fore.CYAN + "Enter the string to search for: " + Style.RESET_ALL).strip()

    
    if not os.path.isfile(file_path):
        print(Fore.RED + f"File not found: {file_path}" + Style.RESET_ALL)
        return

    
    if file_path.endswith('.csv'):
        search_in_csv(file_path, search_string)
    elif file_path.endswith('.txt'):
        search_in_txt(file_path, search_string)
    else:
        print(Fore.RED + "Unsupported file type. Please provide a CSV or TXT file." + Style.RESET_ALL)

if __name__ == "__main__":
    main()
