CC := gcc
CFLAGS := -Wall -Wextra -Wpedantic -Wvla -O0 -std=c23

.PHONY: all clean fmt

all: control_access_below_red_zone

fmt:
	clang-format --style='{IndentWidth: 4, AllowShortFunctionsOnASingleLine: false}' -i *.c

clean:
	rm -f *.a *.o *.abisan.* control_access_below_red_zone

control_access_below_red_zone.o: control_access_below_red_zone.s
	python3 ../../instrument.py control_access_below_red_zone.s
	$(CC) -c $(CFLAGS) $^.abisan.s -o $@

control_access_below_red_zone: main.c control_access_below_red_zone.o ../../libabisan_runtime.a
	$(CC) $(CFLAGS) $^ -o $@
