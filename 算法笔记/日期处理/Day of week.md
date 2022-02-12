```c++
#include<iostream>
#include<string>

/*判断是否是闰年*/
bool is_leap(int year) {
	return ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0) ? true : false;
}

class date {
public:
	int year, month, day; /*直接更改会有隐患*/
	date(int Year = 0, int Month = 1, int Day = 1) :year(Year), month(Month), day(Day) {}

	bool operator<(const date& d) {
		if (year != d.year) return year < d.year;
		if (month != d.month) return month < d.month;
		if (day != d.day) return day < d.day;
		return false;
	}
	bool operator>(const date& d) {
		if (year != d.year) return year > d.year;
		if (month != d.month) return month > d.month;
		if (day != d.day) return day > d.day;
		return false;
	}
	
	date& operator=(const date& d) {
		this->year = d.year;
		this->month = d.month;
		this->day = d.day;
		return *this;
	}



	/*前置递增运算*/
	date& operator++() {
		if (day < this->getDays()) day++;
		else { day = 1; if (++month > 12) month = 1, year++; }
		return *this;
	}


	/*返回所处月份的总天数*/
	int getDays() {
		if (month < 1 || month>12) return -1;
		else if (month == 2) return is_leap(year) ? 29 : 28;
		else return DAYS[month - 1];
	}

	/*求两个日期的差,如果两个日期是连续的，规定相差1天*/
	int operator-(const date& d) {
		int ret = 0;
		date late, early;
		*this > d ? (late = *this, early = d) : (early = *this, late = d);
		/*跳年*/
		while (late.year - early.year > 1) {
			if (early.month <= 2) {
				if (early.month == 2 && early.day == 29) { ret += 365; early.day = 28; }
				else ret += is_leap(early.year) ? 366 : 365;
			}
			else if (early.month > 2) ret += is_leap(early.year + 1) ? 366 : 365;
			early.year++;
		}
		/*跳到次月一日*/
		if (late.year > early.year || (late.year == early.year && late.month > early.month)) {
			ret += early.getDays() - early.day + 1; early.day = 1;
			if (++early.month > 12) early.month = 1, early.year++;
		}
		/*跳日*/
		while (early < late) { ++early; ++ret; }
		return *this > d ? ret : -ret;
	}

private:
	/*二月单独讨论*/
	const int DAYS[12] = { 31,0,31,30,31,30,31,31,30,31,30,31 };
};


int main() {
	
	int day, y,m;
	std::string month;
	date base(2000, 1, 2);

	while (std::cin >> day >> month >> y) {

		if (month == "January") m = 1;
		else if (month == "February") m = 2;
		else if (month == "March") m = 3;
		else if (month == "April") m = 4;
		else if (month == "May") m = 5;
		else if (month == "June") m = 6;
		else if (month == "July") m = 7;
		else if (month == "August") m = 8;
		else if (month == "September") m = 9;
		else if (month == "October")m = 10;
		else if (month == "November")m = 11;
		else if (month == "December")m = 12;
		else std::cout << "error: illegal month" << std::endl;
		date d(y, m, day);
		int diff = d - base;
		while (diff < 0)diff += 7;
		std::string ans;
		switch (diff % 7) {
		case 0:ans = "Sunday"; break;
		case 1:ans = "Monday"; break;
		case 2:ans = "Tuesday"; break;
		case 3:ans = "Wednesday"; break;
		case 4:ans = "Thursday"; break;
		case 5:ans = "Friday"; break;
		case 6:ans = "Saturday"; break;
		}
		std::cout << ans << std::endl;
	}
	
	return 0;
}
```

