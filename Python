import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # TO DO: get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
    
    city = input("Please Enter The City Name (chicago, new york city, washington): ").lower()
    while city not in ('chicago','new york city','washington'):
        print("Sorry Invalid City try again")
        city = input("Please Enter The City Name (chicago, new york city, washington): ")
         
    # TO DO: get user input for month (all, january, february, ... , june)
    month = input("Please Enter The month Name (all, january, february, ... , june): ").lower()
    while month not in ('all','january','february','march','april','may','june'):
        print("Sorry Invalid month try again")
        month = input("Please Enter The month Name (all, january, february, ... , june): ")

    # TO DO: get user input for day of week (all, monday, tuesday, ... sunday)
    day = input("Please Enter The day Name (all, monday, tuesday, ... , sunday): ").lower()
    while day not in ('all','monday','tuesday','wednesday','thursday','friday','saturday','sunday'):
        print("Sorry Invalid day try again")
        day = input("Please Enter The day Name (all, monday, tuesday, ... , sunday): ")
    
    


    print('-'*40)
    return city, month, day


def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """
    #Reading the Data from the CSV file 
    df = pd.read_csv(CITY_DATA[city]) 
    # convert the start time column to datetime
    df['Start Time'] = pd.to_datetime(df['Start Time'])

    # extract month and day of week and hour
    df['month'] = df['Start Time'].dt.month
    df['day_of_week'] = df['Start Time'].dt.weekday_name
    df['hour'] = df['Start Time'].dt.hour 
# filter by month if applicable
    if month != 'all':
        # use the index of the months list to get the corresponding int
        months = ['january', 'february', 'march', 'april', 'may', 'june']
        month = months.index(month) + 1

        # filter by month to create the new dataframe
        df = df[df['month'] == month]

    # filter by day of week if applicable
    if day != 'all':
        # filter by day of week to create the new dataframe
        df = df[df['day_of_week'] == day.title()]

    return df


def time_stats(df):
    """Displays statistics on the most frequent times of travel."""

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # TO DO: display the most common month
    most_common_month = df['month'].mode()[0]
    print(' The Most Freuent Month to Travel : {}'.format(most_common_month))

    # TO DO: display the most common day of week
    most_common_day = df['day_of_week'].mode()[0]
    print(' The Most Freuent day to Travel : {}'.format(most_common_day))

    # TO DO: display the most common start hour
    most_common_hour = df['hour'].mode()[0]
    print(' The Most Freuent hour to Travel : {}'.format(most_common_hour))

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # TO DO: display most commonly used start station
    most_start_station = df['Start Station'].mode()[0]
    print('Most used start station is : {}'.format(most_start_station))

    # TO DO: display most commonly used end station
    most_end_station = df['End Station'].mode()[0]
    print('Most used end station is : {}'.format(most_end_station))

    # TO DO: display most frequent combination of start station and end station trip
    
    print('Most used start and end station is : {} , {}'.format(most_start_station,most_end_station))

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # TO DO: display total travel time
    total_travel_time = df['Trip Duration'].sum()
    print('Total Travel Time = {}'.format(total_travel_time))
    # TO DO: display mean travel time
    mean_travel_time = df['Trip Duration'].mean()
    print('Average Travel Time = {}'.format(mean_travel_time))      

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # TO DO: Display counts of user types
    count_user_type = df['User Type'].value_counts()
    print('Number of user types = {}'.format(count_user_type))
    # TO DO: Display counts of gender
    if 'Gender' in df:
    # Only access Gender column in this case 
        count_gender = df['Gender'].value_counts()
        print('Type and number of gender : {} '.format(count_gender))
    # TO DO: Display earliest, most recent, and most common year of birth
        most_earliest = df['Birth Year'].min()
        most_recent = df['Birth Year'].max()
        most_common = df['Birth Year'].mode()[0]
        print('Most Earliest year of birth : {}\nMost Recent Year of birth : {}\nMost Common year of birth = {}'.format(most_earliest,most_recent,most_common))
    else: 
        print('Gender stats and birth year cannot be calculated because Gender and birth year do not appear in the dataframe')

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)
    
def data_view(df):
    view_data = input("Would you like to view 5 rows of individual trip data? Enter yes or no?").lower()
    start_loc = 5
    while view_data != 'no' :
        print(df.iloc[0:start_loc])
        start_loc += 5
        view_display = input("Do you wish to continue?: ").lower()
        if view_display != 'yes':
            break
        
    


def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)

        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        data_view(df)

        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break


if __name__ == "__main__":
	main()
