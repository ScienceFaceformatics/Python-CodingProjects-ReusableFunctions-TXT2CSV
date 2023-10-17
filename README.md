# txt_2_csv_function
This is a reusable function which takes any comma separated .txt file and converts it into a tabular format (.csv) for ease-of-viewing as a Pandas dataframe or viewing within Excel.

An example file 30_uM_NADP.txt has been provided so that you can test these set of functions out, please download it and then use the code provided to grab/load the file(s) (get_files function) and then parse them into
a Pandas- or Excel-ready .csv format (file_parser function). 

A few things to note:

1. global variables 'in_dir' and 'out_dir' have been assigned to clairfy where the original .txt file is located (in_dir) and the parsed .csv file (out_dir) are located. Change/streamline the code as necessary.

2. You can use the get_files and file_parser functions independently. I have only grouped them into the one .ipynb (Jupyter Notebook) file as these functions formed part of the data cleaning
   section of a broader pipeline I coded for a project.

    For example:

   --- get_files function -----
   
   def get_files(in_dir, out_dir):
      txt_files = glob.glob(in_dir+'*')
      for file in txt_files:
          if os.path.isfile(file):
              if pathlib.Path(f'{file}').suffix != '.txt':
                  txt_files.remove(file)
          elif os.path.isdir(file):
              txt_files.remove(file)
      return txt_files
  txt_files= get_files(in_dir, out_dir)

  ---> this returns txt_files and feeds it as an argument into the file_parser function. HOWEVER, you can create a list of the specific .txt file paths you would like and pass them into the file_parser function instead.
  ----> e.g. txt_files = ['/path/to/directory/foo.txt', '/path/to/directory/bar.txt']

  def file_parser(txt_files, out_dir):

  .....................

  3. Change the value of the 'delimiter' argument in the csv.reader() argument according to how the data is separated. e.g. ',' for commas, '\t' for tabs. Google some of the regex for delimiters, you'll find them.

  4. This code assumes all data values have the same type of delimiter separating them. For more complex .txt files, it'd be best to use the csv.Sniffer().sniff method to check all possible
     delimiters within the file. In addition, csv.Sniffer().has_header can be used to *predict* (term used very lightly) which elements within the file are deemed columns/headers based on their character (e.g. string,
     integer, etc) and length.
