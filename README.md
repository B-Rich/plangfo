# plangfo

 plangfo is a module with some tools. It only has the blob languages detection thing right now tho :P

## Insallation
`pip3 install plangfo`    

## Usage
Add `alias plangfo='python3 -m plangfo'` to your `.bashrc`

And just use it. Go to a directory, type `plangfo`

Here is a test repo:
![output](https://i.imgur.com/1lPnLTw.png)

Here is my output:
![plangfo_output](https://i.imgur.com/qXsL90M.png)

### Arguments/specifying directories
To specify a directory, you need to specify an argument, and vice versa.

To do that, use `plangfo [option] [directory]`

| Arguments |                     |
| --------- | ------------------- |
| a         | --all-files         |
| b         | --bytes             |
| p         | --percentage        |
| sp        | --sorted-percentage |


# TODO:
| TODO      |                     |
| --------- | ------------------- |
| sb        | --sorted-bytes      |


# Languages

If you're wondering how I got that large data of languages. Then, no, of course I didn't make it myself.

I used `wget` to download [languages.yml](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)

`wget https://raw.githubusercontent.com/github/linguist/master/lib/linguist/languages.yml`

Then, a Python script to generate a dictionary.

```python
import yaml
with open("languages.yml") as f:
    dataMap = yaml.safe_load(f)

file = open("data.py", "a+")
file.seek(0)
file.truncate()
file.write("languages = {\n")

for language in dataMap:
    try:
        file.write("\t\"" + language + "\"" + ": " + str(dataMap[language]["extensions"]) + ",\n")
    except KeyError:
        continue
file.write("\t}")
```

The result is, as expected, `data.py`.

Here is the script running on `/`:
```
[dizaztor@DizAzTor /]$ time plangfo 
{'Roff': 24.8, 'HTML': 13.2, 'Modelica': 10.5, 'C++': 7.2, 'C': 6.9, 'Objective-C': 6.2, 'JavaScript': 5.0, 'Python': 4.5, 'Pickle': 3.0, 'SVG': 2.1, 'Go': 2.0, 'XML': 1.8, 'YAML': 1.3, 'JSON': 1.2, 'Text': 1.0, 'Perl': 0.9, 'C#': 0.8, 'Perl 6': 0.7, 'TypeScript': 0.6, 'XPM': 0.6, 'Vim script': 0.6, 'Gettext Catalog': 0.5, 'GCC Machine Description': 0.4, 'Markdown': 0.4, 'CSS': 0.2, 'AMPL': 0.2, 'Linux Kernel Module': 0.2, 'Modula-2': 0.2, 'Ruby': 0.2, 'Pod': 0.2, 'RenderScript': 0.2, 'Rust': 0.2, 'desktop': 0.1, 'Scheme': 0.1, 'Prolog': 0.1, 'reStructuredText': 0.1, 'QML': 0.1, 'Unix Assembly': 0.1, 'CMake': 0.1, 'Gerber Image': 0.1, 'M4': 0.1, 'M4Sugar': 0.1, 'Max': 0.1, 'Tcl': 0.1, 'Java': 0.1, 'Assembly': 0.1, 'PAWN': 0.1, 'PHP': 0.1, 'POV-Ray SDL': 0.1, 'Pascal': 0.1, 'SQL': 0.1, 'SourcePawn': 0.1}

real    5m11.637s
user    4m8.357s
sys 0m8.797s
[dizaztor@DizAzTor /]$ 
```