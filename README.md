```java
/**
 * 如果业务只需要日期，请使用LocalDate,因为LocalDate仅仅关心日期，更专业，也减少了不必要的资源消耗；如果业务只关心时间，那么使用LocalTime
 *
 * 如果业务需要日期时间都要使用，那么可以使用LocalDateTime,DateTime这两个类，它们都是线程安全的同时都是不可变的，使用起来不用担心出问题。
 * LocalDateTime是与时区无关的。
 * DateTime是与时区相关的一个国际标准时间。
 */
public class JodaTest {
    public static void main(String[] args) {
        DateTime dateTime = new DateTime();
        int dayOfMonth = dateTime.getDayOfMonth();
        System.out.println("dayOfMonth=" + dayOfMonth);//dayOfMonth=15

        int dayOfWeek = dateTime.getDayOfWeek();
        System.out.println("dayOfWeek=" + dayOfWeek);//dayOfWeek=5

        int dayOfYear = dateTime.getDayOfYear();
        System.out.println("dayOfYear=" + dayOfYear);//dayOfYear=349

        int hourOfDay = dateTime.getHourOfDay();
        System.out.println("hourOfDay=" + hourOfDay);//hourOfDay=17

        long millis = dateTime.getMillis();
        System.out.println("millis=" + millis);//millis=1513329501701

        int millisOfDay = dateTime.getMillisOfDay();
        System.out.println("millisOfDay=" + millisOfDay);//millisOfDay=62301701

        int millisOfSecond = dateTime.getMillisOfSecond();
        System.out.println("millisOfSecond=" + millisOfSecond);//millisOfSecond=701

        int minuteOfDay = dateTime.getMinuteOfDay();
        System.out.println("minuteOfDay=" + minuteOfDay);//minuteOfDay=1038

        int minuteOfHour = dateTime.getMinuteOfHour();
        System.out.println("minuteOfHour=" + minuteOfHour);//minuteOfHour=18

        int monthOfYear = dateTime.getMonthOfYear();
        System.out.println("monthOfYear=" + monthOfYear);//monthOfYear=12

        int secondOfDay = dateTime.getSecondOfDay();
        System.out.println("secondOfDay=" + secondOfDay);//secondOfDay=62301

        int secondOfMinute = dateTime.getSecondOfMinute();
        System.out.println("secondOfMinute=" + secondOfMinute);//secondOfMinute=21

        int weekOfWeekyear = dateTime.getWeekOfWeekyear();
        System.out.println("weekOfWeekyear=" + weekOfWeekyear);//weekOfWeekyear=50

        int weekyear = dateTime.getWeekyear();
        System.out.println("weekyear=" + weekyear);//weekyear=2017

        int year = dateTime.getYear();
        System.out.println("year=" + year);//year=2017

        int yearOfCentury = dateTime.getYearOfCentury();
        System.out.println("yearOfCentury=" + yearOfCentury);//yearOfCentury=17

        DateTime dateTime2 = new DateTime(2017,9,14,20,30,0);
        System.out.println("明确给出年月日时分秒=" + dateTime2);//明确给出年月日时分秒=2017-09-14T20:30:00.000+08:00

        DateTime dateTime3 = new DateTime(1505371053358L);
        System.out.println("通过时间戳创建=" + dateTime3);//通过时间戳创建=2017-09-14T14:37:33.358+08:00

        String date = "2017-09-14 20:30:00";
        DateTimeFormatter dateTimeFormatter = DateTimeFormat.forPattern("yyyy-MM-dd HH:mm:ss");
        DateTime dateTime4 = dateTimeFormatter.parseDateTime(date);
        System.out.println("通过字符串构造=" + dateTime4);//通过字符串构造=2017-09-14T20:30:00.000+08:00

        DateTime dateTime6 = new DateTime(DateTimeZone.forTimeZone(TimeZone.getTimeZone("Asia/Shanghai")));
        System.out.println("指定时区构造=" + dateTime6);//指定时区构造=2017-12-15T17:47:58.327+08:00

        DateTime dateTime7 = new DateTime();
        DateTimeZone zone = dateTime7.getZone();
        System.out.println("获取时区=" + zone);//获取时区=Asia/Shanghai

        DateTime dateTime8 = new DateTime();
        DateTime theFirstDateOfMonth = dateTime8.dayOfMonth().withMinimumValue();
        System.out.println("月第一天=" + theFirstDateOfMonth);//月第一天=2017-12-01T17:47:58.327+08:00

        DateTime theEndDataOfMonth = dateTime8.dayOfMonth().withMaximumValue();
        System.out.println("月最后一天=" + theFirstDateOfMonth);//月最后一天=2017-12-01T17:47:58.327+08:00

        int day = dateTime8.getDayOfMonth();
        System.out.println("几号=" + day);//几号=15

        int month = dateTime8.getMonthOfYear();
        System.out.println("几月=" + month);//几月=12

        int year2 = dateTime8.getYear();
        System.out.println("哪年=" + year2);//哪年=2017
        if(dateTime8.getDayOfMonth() == DateTimeConstants.SEPTEMBER){
        }

        // 获取相对于当前时间的月份，比如获取上个月的时间或者下个月的是时间，方法minusMoths接受一个int的参数，如果这个参数等于0，代表本月，大于0代表已经过去的时间，小于0代表还没有到来的时间
        DateTime lastDayOfMonth = new DateTime().minusMonths(1).dayOfMonth().withMaximumValue();
        System.out.println("获取上个月最后一天=" + lastDayOfMonth);//获取上个月最后一天=2017-11-30T17:47:58.328+08:00

        DateTime firstDayOfMonth = new DateTime().minusMonths(1).dayOfMonth().withMinimumValue();
        System.out.println("获取上个月第一天=" + firstDayOfMonth);//获取上个月第一天=2017-11-01T17:47:58.328+08:00

        DateTime dateTime9 = new DateTime();
        int week = dateTime9.getDayOfWeek();
        System.out.println("星期几=" + week);//星期几=5

        if(dateTime9.getDayOfWeek() == DateTimeConstants.WEDNESDAY){
            // 判断今天是不是星期三
        }

        DateTime currentDateTime = new DateTime();
        DateTime targetDateTime = new DateTime(2017,10,1,0,0,0);

        int years = Years.yearsBetween(currentDateTime,targetDateTime).getYears();
        System.out.println("相差多少年=" + years);//相差多少月=-2

        int months = Months.monthsBetween(currentDateTime,targetDateTime).getMonths();
        System.out.println("相差多少月=" + months);//相差多少月=-2

        int days = Days.daysBetween(currentDateTime,targetDateTime).getDays();
        System.out.println("距离国庆放假多少天=" + days);//距离国庆放假多少天=-75

        int hours = Hours.hoursBetween(currentDateTime,targetDateTime).getHours();
        System.out.println("距离国庆放假多少小时=" + hours);//距离国庆放假多少小时=-1817

        int minutes = Minutes.minutesBetween(currentDateTime,targetDateTime).getMinutes();
        System.out.println("距离国庆放假多少分钟=" + minutes);//距离国庆放假多少小时=-1817

        int seconds = Seconds.secondsBetween(currentDateTime,targetDateTime).getSeconds();
        System.out.println("距离国庆放假多少秒=" + seconds);//距离国庆放假多少秒=-6544078


        int weeks = Weeks.weeksBetween(currentDateTime,targetDateTime).getWeeks();
        System.out.println("距离国庆放假多少周=" + weeks);//距离国庆放假多少周=-10


        System.out.println("今天的零点=" + currentDateTime.withMillisOfDay(0));
        //今天的零点=2017-12-15T00:00:00.000+08:00

        System.out.println("昨天的零点=" + currentDateTime.withMillisOfDay(0).plusDays(-1));
        //昨天的零点=2017-12-14T00:00:00.000+08:00

        System.out.println("明天的零点=" + currentDateTime.withMillisOfDay(0).plusDays(1));
        //明天的零点=2017-12-16T00:00:00.000+08:00

        System.out.println("这一年最后一天0点=" + new DateTime().dayOfYear().withMaximumValue().withMillisOfDay(0));
        //这一年最后一天0点=2017-12-31T00:00:00.000+08:00

        System.out.println("这一年第一天0点=" + new DateTime().dayOfYear().withMinimumValue().withMillisOfDay(0));
        //这一年第一天0点=2017-01-01T00:00:00.000+08:00

        System.out.println("这个月最后一天0点=" + new DateTime().dayOfMonth().withMaximumValue().withMillisOfDay(0));
        //这个月最后一天0点=2017-12-31T00:00:00.000+08:00

        System.out.println("这个月月初0点=" + new DateTime().dayOfMonth().withMinimumValue().withMillisOfDay(0));
        //这个月月初0点=2017-12-01T00:00:00.000+08:00

        DateTime currentDateTime3 = new DateTime();
        String s = currentDateTime3.toString("yyyy-MM-dd HH:mm:ss");
        System.out.println("格式化=" + s);//格式化=2017-12-15 17:47:58

        LocalDate localDate = new LocalDate();
        LocalTime localTime = new LocalTime();
        System.out.println("日期=" + localDate);//日期=2017-12-15
        System.out.println("时间=" + localTime);//时间=17:47:58.425
    }
}
```