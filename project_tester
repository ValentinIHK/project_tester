#!/usr/bin/python3

import sys
import os
import subprocess


# Error handling


def help():
    print("\t-- Python project tester --\n")
    print("This script will help you to compare your project with another one.\n")
    print("USAGE:")
    print("\t./test_me [binary 1] [binary 2] [arguments file]\n")
    print("Made by valentin.ichkour@epitech.eu")
    exit(84)


def check_open_file():
    try:
        open(sys.argv[1], 'r')
        open(sys.argv[2], 'r')
    except IOError:
        sys.stderr.write('Error: Could not found one of your binary\n')
        exit(84)


def start_script():
    arglist = ""
    errors = []

    for i in sys.argv[3:]:
        arglist += " " + i
    try:
        binary1 = "./" + sys.argv[1] + " " + arglist
        binary2 = "./" + sys.argv[2] + " " + arglist
        try:
            output1 = subprocess.Popen([binary1], stdout=subprocess.PIPE, shell=True).communicate()[0].decode('ascii').split('\n')
            output2 = subprocess.Popen([binary2], stdout=subprocess.PIPE, shell=True).communicate()[0].decode('ascii').split('\n')
        except CalledProcessError:
            exit(84)

        for data_res1 in range(0, len(output1)):
            if output1[data_res1].replace("\t", "").replace(" ", "") != output2[data_res1].replace("\t", "").replace(" ", ""):
                errors.append("binary 1 => " + output1[data_res1])
                errors.append("binary 2 => " + output2[data_res1])
                if errors:
                    print("Arguments =>" + arglist)
                    print("<------------------------------>")
                    for err in errors:
                        print(err)
        if not errors:
            print("No errors. Well done !")
    except IOError:
        print("An error has occured during tests")
        exit(84)


# Core


def core():
    try:
        start_script()
    except IndexError:
        print("Error: List index out of range.")
        exit(84)
    except IOError as e:
        print ("I/O error({}): {}".format(e.errno, e.strerror))
        exit(84)
    except ValueError:
        print ("Could not convert data to an integer.")
        exit(84)
    except OverflowError:
        print("Math range error.")
        exit(84)


# Main


if __name__ == '__main__':
    if len(sys.argv) < 3 or sys.argv[1] == "-h":
        help()
    else:
        core()
