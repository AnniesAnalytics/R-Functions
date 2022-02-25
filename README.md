# R-Functions
This is where I am keeping the R functions I am learning!

# R Functions

A good webpage explaining some basic concepts:http://varianceexplained.org/RData/code/code_lesson2/

# Assignment operator
An assignment operator is <-
Arrange
To arrange your data in your table according to a specification, such as length (it will then sort it in ascending order. EX:
arrange(filtered_tg,len)

Penguins %/% arrange(bill_length_mm)
TO make it in descending order :  penguins %/% arrange(-bill_length_mm_)

You could also use the desc command:
arrange(hotel_bookings, desc(lead_time))  OR  arrange(hotel_bookings, -lead_time)
Then to save it in that order
hotel_bookings_v2 <- arrange(hotel_bookings, desc(lead_time))

# Bias
You can check for bias in your datasets. You need to first install the Sim package
install.packages(“SimDesign”)    library(SimDesign)
Then, get the data that you are using by either uploading or creating it. Then you can use the function. It will return a number. If it is close to 0 it is close to unbiased. It is not out of 1 like correlation. If it is negative, the predicted outcome is larger than the actual outcome.
bias(actual_temp,predicted_temp)   - just input the two columns you want to compare.

# Clean_names
This function allows you to make sure your column names only contain numbers, letters, and _. No spaces. 
clean_names(penguins)

# Colnames
colnames() will return the names of each of the columns of your dataset. When it returns you a number in [] at the beginning of a new line of names, that indicates the # column you are up to. 
colnames(diamonds)     

# Data
To load your data use data
data(“name”)

To load the data frame and then preview it in the R console after it is loaded type its name and then press CTRL+Enter
You can also display the dataset by clicking directly on the name of the dataset in the Environment pane

# Data.Frame
This allows you to create a data frame right in R. First, create a vector of names by inserting four names into this code block between the quotation marks and then run it:

names <- c("", "", "", "")

Then create a vector of ages by adding four ages separated by commas to the code chunk below. Make sure you are inputting numeric values for the ages or you might get an error. 
age <- c(, , , )
With these two vectors, you can create a new data frame called `people`:
people <- data.frame(names, age)

Ex:
Fruits <- c("apple", "banana", "orange", "berry")
Rank <- c(3, 4, 2, 1)
fruit_ranks <- data.frame(Fruits, Rank)
head(fruit_ranks)
=
 Fruits Rank
1  apple    3
2 banana    4
3 orange    2
4  berry    1

Another ex: adr is average daily rate 
new_df <- select(bookings_df, `adr`, adults)

mutate(new_df, total = `adr` / adults)
This changes the frame and not the original. 


# Drop na
Use this function if you want to drop blank rows from your data frame. 
Penguins %/% group_by(island) %/% drop_na() %/% summarize(mean_bill_length_mm = mean(bill_length_mm))


# Filter
To filter the data you see from a table, use filter. The == means find an exact match.
New_name <- filter(OldName, specification==number)
filtered_tg <- filter(ToothGrowth,dose==0.5)

You do not have to rename, you can just filter the rows out of the dataset.
Penguins %/% filter(species == “Adelie”)

filter(hotel_bookings, hotel_bookings$hotel=="City Hotel") 
In this one, the hotel_bookings is dataset name and hotel is the column.

To filter using a pipe:
onlineta_city_hotels_v2 <- hotel_bookings %>%
  filter(hotel=="City Hotel") %>%
  filter(market_segment=="Online TA")

filter(Cocoa.Percent>=70) %>%
filter(Rating==3.5)



## GGplot see other sheet
# ggsave
sAve your plot using ggsave(“_.png”)

# Glimpse
glimpse() Glimpse returns a summary of your data aligned horizontally
glimpse(diamonds)      

# Group By
This groups your data by values in a certain column. group_by(columnName, columnName2)

# Head
head() displays the columns and first few rows of data. Ex:     
head(diamonds)

# Markdown
When saving a file in markdown, you can make code chunks:
All code chunks begin and end with delimiters. To start a code chunk, you can type three tick marks followed by a lowercase “r” in curly brackets: ```{r} 

To end it, type just the three tick marks: ```

There are two shortcuts to adding code. On your keyboard, you can press Ctrl + Alt + I (PC) or Cmd + Option + I (Mac). Or you can click the Add Chunk command in the editor toolbar. Its a C with a green plus on it.
To add a code chunk to your Rmd file, follow these steps: 
Click the end of the last line of your Rmd file. Use either of the previously-mentioned shortcuts to create a code chunk
 Press Enter (Windows) or Return (Mac) two or three times after the default code chunk to create space between the existing code chunk and the next code chunk you will add.
 Copy the code from the analysis file you opened earlier and paste it in the gray area between the beginning and ending delimiters. 
 Select the rest of the template content in the file and delete it. This gives you a blank space to work in to help avoid potential errors from mixing your own comments and code with the pre-existing ones in the template.
The white background is where you will type plain text with markdown syntax.
*space makes a bullet
Click here[link] (insert link)


# Min/Max/Mean
You can find the min/max/mean in a column by using these functions. You need to use a $ between dataset name and column name or you will get an error.
min(hotel_bookings$lead_time)

# Mutate
Allows us to make changes to our data. For example, to see people’s ages (from age column) in 20 years- it makes a new column from age:
mutate(people, age_in_20 = age + 20)

Here is another example:
Penguins %/% 
mutate(body_mass_kg=body_mass_g/1000, flipper_length_m=flipper_length_mm/1000)

## Nested Functions
You can nest one function within another. In this example, it will first filter the data, and then arrange it by length. 
arrange(filter(ToothGrowth,dose==0.5),len)

# Pipe
To insert a pipe operator %>% you can press ctrl+shft+M

# Readr
read_csv(): comma-separated values (.csv) files
read_tsv(): tab-separated values files
read_delim(): general delimited files
read_fwf(): fixed-width files
read_table(): tabular files where columns are separated by white-space
read_log(): web log files
bookings_df <- read_csv("hotel_bookings.csv")
When you use Readr on a CSV,  R prints out a column specification that gives the name and type of each column. It also prints a tibble. 

# Readxl
The readxl package is part of the tidyverse but is not a core tidyverse package, so you need to load readxl in R by using the library() function.  
library(readxl)
You can use the read_excel() function to read a spreadsheet file just like you used read_csv() function to read a  .csv file. The code for reading the example file “type-me.xlsx” includes the path to the file in the parentheses of the function.  
read_excel(readxl_example("type-me.xlsx"))
You can use the excel_sheets() function to list the names of the individual sheets. 
 excel_sheets(readxl_example("type-me.xlsx"))
[1] "logical_coercion" "numeric_coercion" "date_coercion" "text_coercion"
You can also specify a sheet by name or number.  Just type “sheet =” followed by the name or number of the sheet. For example, you can use the sheet named “numeric_coercion” from the list above. 
read_excel(readxl_example("type-me.xlsx"), sheet = "numeric_coercion")
When you run the function, R returns a tibble of the sheet. 

# Rename
This allows you to rename column names. Ex: Where carat and cut were the ORIGINAL names.
rename(diamonds, carat_new = carat, cut_new = cut)
This is backwards from SQL

# Rename_with
This function allows you to do some cleaning all at once. So you can change the column names all at once by using rename_with(dataname,condition)
rename_with(penguins,tolower)
Also see clean names

Here it is as a pipe where you have created a new data frame and renamed them:
trimmed_df %>% 
  select(hotel, is_canceled, lead_time) %>% 
  rename(hotel_type = hotel)


# Select 
To select the columns you want to see, or all of them except certain ones, you can use select.
Use the name of your data set, start a pipe, then the command. Name  %/% select(column) ex:
Penguins %/%
    select(species) 
To see all except one, you can use - . select(-species) 

If you want to create a new dataframe that only contains the columns you are looking for:
trimmed_df <- bookings_df %>% 
  select(hotel, is_canceled, lead_time)

# Separate (CONCAT)
separate(employee, name,into=c('first_name','last_name'), sep=' ')
Its partner is unite.

# Summarize data
summarize(diamonds, mean_carat = mean(carat))

Penguins %/% group_by(species, island) %/% drop_na() %/% summarize(mean_bill_length_mm = mean(bill_length_mm, max_bl = max(bill_length_mm))
Mean_bill_length_mm is the NEW name. 
You could also replace the word mean with things such as max or min

# max/min/mean/sum

hotel_summary <- 
  hotel_bookings %>%
  group_by(hotel) %>%
  summarize(average_lead_time=mean(lead_time),
            min_lead_time=min(lead_time),
            max_lead_time=max(lead_time))

example_df <- bookings_df %>%
  summarize(number_canceled = sum(is_canceled),
            average_lead_time = mean(lead_time))

Another ex were sd is standard deviation and cor is correlation.
Quartet %/%
	group_by(set) %/%
	summarize(mean(x),sd(x),mean(y),sd(y),cor(x,y))



# STR
str()  Returns a summary of your data aligned horizontally ex (stands for structure)
str(diamonds)

# Tidyverse
install.packages("tidyverse")
library(tidyverse)

# Tibble
You can create a Tibble- which is a like a streamlined data frame, using:
as_tibble()



# Unite
This will combine data from two columns into one. Here we create a new df called example_df which is made out of a previously created df called bookings_df that had cleaner column names. You have to first call up and select the columns you want, and then you can combine them and give them a new name. 

example_df <- bookings_df %>%
  select(arrival_date_year, arrival_date_month) %>% 
  unite(arrival_month_year, c("arrival_date_month", "arrival_date_year"), sep = " ")

The new name is arrival_month_year. The date month and date year are being combined. You are separating them using a space hence the “ “

Another example where name is the new column name:
unite(employee, ‘name’, first_name,last_name,sep=’ ‘)


# View
To view the data in a separate pane, use View()
View(filtered_tg)


