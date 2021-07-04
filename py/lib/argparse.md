# argparse

## Basics

```py
import argparse

parser = argparse.ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                    help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))
```

* metavar: A name for the argument in usage messages.
* nargs: The number of command-line arguments that should be consumed. (int val, ?(1 or not) - optional, *(0 or more), +(1 or more))
* dest: The name of the attribute to be added to the object returned by `parse_args()`.
* action: The basic type of action to be taken when this argument is encountered at the command line.
  - store_const: This stores the value specified by the `const` keyword argument.

## Subcommands

Use `add_subparsers` and `set_defaults`.

```py
import argparse

def add(args):
    x, y = args.integers
    print(x + y)

def sub(args):
    x, y = args.integers
    print(x - y)

parser = argparse.ArgumentParser()
subparsers = parser.add_subparsers()

parser_add = subparsers.add_parser('add')
parser_add.add_argument('integers', nargs=2, type=int)
parser_add.set_defaults(func=add)

parser_sub = subparsers.add_parser('sub')
parser_sub.add_argument('integers', nargs=2, type=int)
parser_sub.set_defaults(func=sub)

args = parser.parse_args()
args.func(args)
```
