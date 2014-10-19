# Manual Duplex Printing

Small bash script to print documents two-sided with a single-sided printer.

## Installation

Clone the repository to any location you like and place the directory on your `PATH`.

### ZSH autocompletion:

If you are using the Z-Shell, you can enable autocompletion by adding this to your `.zshrc`:
```
compdef lprdup=lpr
```

## Usage

The script is intended for manual double-sided printing on a single-sided printer.
It will print the first set of pages that go on one side, then prompt the user to hit enter to print the other side.
Depending on how your printer operates you can configure which subset of pages (even or odd) is printed first, and in which order the pages are printed.
Most Inkjet printers take the topmost empty page from the fresh paper tray and print on the opposite side.
For these printers you:

1. print the odd pages in reverse order
2. place the printed stack of paper in the paper tray with the printed sides up and the top of the pages showing toward the printer (ie. you turn them by 180° after taking them from the printer)
4. print the even pages in normal order

The `lprdup` script facilitates this process.

```
$ lprdup myfile.pdf
printing odd pages in reverse order
when the print job is done:
    1. Take the printed stack of paper (WITHOUT CHANGING ITS ORDER)
    2. Put it in the fresh paper tray. Make sure you use the correct way for your printer.
    3. Hit enter to print the back sides.
$ <hits enter>
printing even pages in normal order
```

You can pass any arguments for `lpr` to the script.

## Printer configuration

Since the correct order of subsets depends on the printer, this can be configured in the `~/.lprdup` file using a string of four characters for each printer.
For the configuration described above this string would be `oren`, indicating that first the *odd* pages are printed in *reverse* order and then the *even* pages are printed in *normal* order.
For a printer named `my-printer` the following line in `~/.lprdup` would set this configuration:

```
printer_config[my-printer]=oren
```

When you use `lprdup` with a printer for which there is no configuration, you will be prompted to enter one.
This configuration will automatically be appended to `~/.lprdup` so you will not have to re-enter it after the first time.

If you explicitly select a printer using the `-P <printer name>` argument, the settings for this printer will be used.
