<template>
  <div id="app" style="margin: 0 auto;">
    <h1>Vue Hotel datepicker@2</h1>

    <div class="box">
      <h3>
        New periods management
      </h3>
      <DatePicker
        ref="DatePicker"
        clickOutsideElementId="clickOutsideElement"
        :firstDayOfWeek="1"
        :showYear="true"
        :format="dateFormat"
        :lastDateAvailable="lastDateAvailable"
        :minNights="1"
        :i18n="frFR"
        :disableCheckoutOnCheckin="true"
        :periodDates="periodDates2"
        @renderNextMonth="renderNextMonth"
      />
    </div>

    <div>
      <div class="box">
        <h3>
          Add new disabledDates when paginate (simulate fetch)
        </h3>
        <DatePicker
          ref="DatePicker"
          :showYear="true"
          clickOutsideElementId="clickOutsideElement"
          :disabledDates="dynamicDisabledDates"
          :format="dateFormat"
          :lastDateAvailable="lastDateAvailable"
          :minNights="minNights"
          :i18n="frFR"
          @renderNextMonth="renderNextMonth"
        />
      </div>

      <div class="box">
        <h3>
          Render next month emit
        </h3>

        <DatePicker
          ref="DatePicker"
          clickOutsideElementId="clickOutsideElement"
          :disabledDates="[]"
          :startingDateValue="
            new Date(
              'Wed May 03 2023 00:00:00 GMT+0200 (heure d’été d’Europe centrale)'
            )
          "
          :endingDateValue="
            new Date(
              'Wed May 10 2023 00:00:00 GMT+0200 (heure d’été d’Europe centrale)'
            )
          "
          :showYear="true"
          :format="dateFormat"
          :lastDateAvailable="lastDateAvailable"
          :minNights="minNights"
          :i18n="frFR"
          :disableCheckoutOnCheckin="true"
          :periodDates="periodDates"
          @renderNextMonth="renderNextMonth"
        />
      </div>
      <div class="box">
        <h3>
          Open DatePicker outside
          <button id="clickOutsideElement" @click="toggleDatePickerOutside">
            Open
          </button>
        </h3>
        <DatePicker
          ref="DatePicker"
          clickOutsideElementId="clickOutsideElement"
          :disabledDates="[]"
          :format="dateFormat"
          :lastDateAvailable="lastDateAvailable"
          :minNights="minNights"
          :i18n="frFR"
        />
      </div>
      <div class="box">
        <h3>
          Show list of static bookings
        </h3>
        <DatePicker
          :alwaysVisible="true"
          :bookings="bookings"
          :disableCheckoutOnCheckin="true"
          :firstDayOfWeek="1"
          :format="dateFormat"
          :hoveringTooltip="false"
          :i18n="frFR"
          :lastDateAvailable="lastDateAvailable"
          :minNights="1"
          :showYear="true"
          @bookingClicked="bookingClicked"
          @periodSelected="periodSelected"
          @handleCheckIncheckOutHalfDay="handleCheckIncheckOutHalfDay"
        />
      </div>
      <div class="box">
        <h3>
          Calendar in full view
        </h3>
        <DatePicker
          :disabledDates="[
            '2021-07-15',
            '2021-07-16',
            '2021-07-17',
            '2021-07-18',
            '2021-07-19',
            '2021-07-20',
            '2021-07-21',
            '2021-08-01',
            '2021-08-02',
            '2021-08-03',
            '2021-08-04',
            '2021-08-11',
            '2021-08-12',
            '2021-08-13',
            '2021-08-14',
            '2021-08-15',
            '2021-08-16',
            '2021-08-17',
            '2021-08-18'
          ]"
          :alwaysVisible="true"
          :format="dateFormat"
          :lastDateAvailable="lastDateAvailable"
          :minNights="minNights"
          :i18n="frFR"
          :showYear="true"
          :firstDayOfWeek="1"
          :disableCheckoutOnCheckin="true"
          @handleCheckIncheckOutHalfDay="handleCheckIncheckOutHalfDay"
        />
      </div>
      <div class="box">
        <h3>
          Show calendar on the right
        </h3>
        <DatePicker
          :disabledDates="[
            '2021-07-15',
            '2021-07-16',
            '2021-07-17',
            '2021-07-18',
            '2021-07-19',
            '2021-08-15',
            '2021-08-16',
            '2021-08-17',
            '2021-08-18',
            '2021-08-19',
            '2021-08-20',
            '2021-08-21',
            '2021-08-22'
          ]"
          :format="dateFormat"
          :lastDateAvailable="lastDateAvailable"
          :minNights="minNights"
          :i18n="frFR"
          :positionRight="true"
          :showYear="true"
          :firstDayOfWeek="1"
          :disableCheckoutOnCheckin="true"
          :periodDates="periodDates"
          @handleCheckIncheckOutHalfDay="handleCheckIncheckOutHalfDay"
        />
      </div>
      <div class="box">
        <h3>
          Display one month only
        </h3>
        <DatePicker
          :disabledDates="[
            '2021-06-15',
            '2021-06-16',
            '2021-06-17',
            '2021-06-18',
            '2021-06-19',
            '2021-06-20',
            '2021-06-21',
            '2021-07-01',
            '2021-07-02',
            '2021-07-03',
            '2021-07-04',
            '2021-07-11',
            '2021-07-12',
            '2021-07-13',
            '2021-07-14',
            '2021-07-15',
            '2021-07-16',
            '2021-07-17',
            '2021-07-18'
          ]"
          :format="dateFormat"
          :showSingleMonth="true"
          :lastDateAvailable="lastDateAvailable"
          :minNights="minNights"
          :i18n="frFR"
          :showYear="true"
          :firstDayOfWeek="1"
          :disableCheckoutOnCheckin="true"
          :periodDates="periodDates"
          @handleCheckIncheckOutHalfDay="handleCheckIncheckOutHalfDay"
        />
      </div>
      <div class="box">
        <h3>
          Insert content with the content slot
        </h3>
        <DatePicker :lastDateAvailable="lastDateAvailable" show-year>
          <!-- Insert content here -->
          <div slot="content">
            Hello
          </div>
        </DatePicker>
      </div>
      <div class="box">
        <h3>
          Last date available
          <strong>lastDateAvailable</strong> props <br />
        </h3>
        <p>Stop pagination two years later</p>
        <DatePicker :lastDateAvailable="lastDateAvailable" />
      </div>
      <div class="box">
        <h3>
          Blocked different day when clicked on with
          <strong>periodDates</strong>&nbsp;
          <span style="font-weight: 400">Emit dayClicked</span>
        </h3>
        <DatePicker
          :disabledDates="[
            '2021-10-15',
            '2021-10-16',
            '2021-10-17',
            '2021-10-18',
            '2021-10-19',
            '2021-10-20',
            '2021-10-21',
            '2021-10-01',
            '2021-10-02',
            '2021-10-03',
            '2021-10-04',
            '2021-10-05',
            '2021-10-06',
            '2021-10-07'
          ]"
          :disableCheckoutOnCheckin="true"
          :minNights="minNights"
          @dayClicked="dayClicked"
        />
      </div>
      <div class="box">
        <h3>Half day, If you have check in at noon and checkout before noon</h3>
        <DatePicker
          :minNights="0"
          :disabledDates="[
            '2021-05-01',
            '2021-05-02',
            '2021-05-03',
            '2021-05-04',
            '2021-05-06',
            '2021-05-07',
            '2021-05-08'
          ]"
        />
      </div>
      <div class="box">
        <h3>Disable check-in and check-out on the same day</h3>
        <DatePicker :disableCheckoutOnCheckin="true" :minNights="0" />
      </div>
      <div class="box">
        <h3>Allow selection of single day</h3>
        <DatePicker :singleDaySelection="true" />
      </div>
      <div class="box">
        <h3>Check in only on saturday and minimum stay of 10 nights</h3>
        <DatePicker
          :disabledDaysOfWeek="[
            'Tuesday',
            'Wednesday',
            'Thursday',
            'Friday',
            'Saturday',
            'Sunday'
          ]"
          :enableCheckout="true"
        />
      </div>
      <div class="box">
        <h3>Block all dates after December 31st of the current year</h3>
        <DatePicker :endDate="new Date(new Date().getFullYear(), 11, 31)" />
      </div>
      <div class="box">
        <h3>Block all dates after September 15th</h3>
        <DatePicker :endDate="new Date(new Date().getFullYear(), 8, 15)" />
      </div>
      <div class="box">
        <h3>Block all date ranges of more than 30 days</h3>
        <DatePicker
          :maxNights="30"
          :showBottomBar="false"
          :selectForward="false"
        />
      </div>
      <div class="box">
        <h3>Minimum stay of 3 days</h3>
        <DatePicker :minNights="3" :showBottomBar="true" />
      </div>
      <div class="box">
        <h3>Certain dates blocked</h3>
        <DatePicker
          :disabledDates="['2017-09-14', '2017-09-26']"
          :showCloseButton="true"
        />
      </div>
      <div class="box">
        <h3>
          Allow setting a default date range ( can be used to set a range from a
          url param )
        </h3>
        <DatePicker
          format="DD/MM/YYYY"
          :startingDateValue="
            new Date(
              new Date().getFullYear(),
              new Date().getMonth(),
              new Date().getDate()
            )
          "
          :endingDateValue="
            new Date(
              new Date().getFullYear(),
              new Date().getMonth(),
              new Date().getDate() + 5
            )
          "
        />
        <h4>
          If starting date is before start of calendar, dates will be cleared
        </h4>
        <DatePicker
          format="DD/MM/YYYY"
          :startingDateValue="
            new Date(
              new Date().getFullYear(),
              new Date().getMonth(),
              new Date().getDate() - 1
            )
          "
          :endingDateValue="
            new Date(
              new Date().getFullYear(),
              new Date().getMonth(),
              new Date().getDate() + 5
            )
          "
        />
      </div>
      <div class="box">
        <h3>Checkin only on saturdays</h3>
        <DatePicker
          :disabledDaysOfWeek="[
            'Monday',
            'Tuesday',
            'Wednesday',
            'Thursday',
            'Friday',
            'Sunday'
          ]"
          :enableCheckout="true"
          :minNights="7"
        />
      </div>
      <div class="box">
        <h3>Custom tooltip text</h3>
        <DatePicker
          tooltipMessage="<strong style='color: red'>Enjoy</strong> your stay!"
        />
      </div>
      <div class="box">
        <h3>Show year</h3>
        <DatePicker :showYear="true" />
      </div>
      <div class="box">
        <h3>Custom date format with i18n (e.g.: pt-PT)</h3>
        <DatePicker format="MMMM D" :i18n="ptPT" />
      </div>
      <div class="box">
        <h3>Change the first day of the week to Monday</h3>
        <DatePicker :firstDayOfWeek="1" />
      </div>
      <div class="box">
        <h3>Set checkIn value</h3>
        <DatePicker :firstDayOfWeek="1" :checkInValue="new Date()" />
      </div>
      <div class="box">
        <h3>Set checkOut value</h3>
        <DatePicker
          :firstDayOfWeek="1"
          :checkInValue="new Date()"
          :checkOutValue="
            new Date(
              new Date().getFullYear(),
              new Date().getMonth(),
              new Date().getDate() + 3
            )
          "
        />
      </div>
      <div class="box">
        <h3>Event CheckIn</h3>
        <DatePicker
          @check-in-changed="checkInChanged($event)"
          @check-out-changed="checkOutChanged($event)"
        />

        new Check In Date : {{ newCheckInDate }} <br />
        new Check Out Date : {{ newCheckOutDate }}
      </div>
      <div class="box">
        <h3>Calendar with bookings</h3>
        <DatePicker
          :alwaysVisible="true"
          :bookings="bookings2"
          clickOutsideElementId="clickOutsideElementId"
          :disableCheckoutOnCheckin="true"
          :disabledDates="[]"
          :endingDateValue="
            new Date(
              'Wed May 10 2023 00:00:00 GMT+0200 (heure d’été d’Europe centrale)'
            )
          "
          :firstDayOfWeek="1"
          :format="dateFormat"
          :checkIncheckOutHalfDay="true"
          :hoveringTooltip="false"
          :i18n="frFR"
          :lastDateAvailable="lastDateAvailable"
          :minNights="minNights"
          :positionRight="true"
          :showYear="true"
        />
      </div>
    </div>
  </div>
</template>

<script>
import DatePicker from "./components/DatePicker/index.vue";

export default {
  components: {
    DatePicker
  },
  data() {
    return {
      dynamicDisabledDates: ["2021-04-30", "2021-05-01", "2021-05-02"],
      ptPT: {
        night: "Noite",
        nights: "Noites",
        "day-names": ["Dom", "Seg", "Ter", "Qua", "Qui", "Sex", "Sab"],
        "check-in": "Partida",
        "check-out": "Chegada",
        "month-names": [
          "Janeiro",
          "Fevereiro",
          "Março",
          "Abril",
          "Maio",
          "Junho",
          "Julho",
          "Agosto",
          "Setembro",
          "Outubro",
          "Novembro",
          "Dezembro"
        ],
        tooltip: {
          halfDayCheckIn: "Reservas possíveis",
          halfDayCheckOut: "Reservas possíveis",
          saturdayToSaturday: "Sábado a Sábado<br/> apenas",
          sundayToSunday: "Domingo a domingo<br/> apenas",
          minimumRequiredPeriod: "%{minNightInPeriod} %{night} mínimo."
        },
        week: "semana",
        weeks: "semanas"
      },
      frFR: {
        "check-in": "Arrivée",
        "check-out": "Départ",
        "day-names": ["lu", "ma", "me", "je", "ve", "sa", "di"],
        "month-names": [
          "Janvier",
          "Février",
          "Mars",
          "Avril",
          "Mai",
          "Juin",
          "Juillet",
          "Août",
          "Septembre",
          "Octobre",
          "Novembre",
          "Décembre"
        ],
        night: "nuit",
        nights: "nuits",
        tooltip: {
          halfDayCheckIn: "Réservation possible",
          halfDayCheckOut: "Réservation possible",
          saturdayToSaturday: "Du samedi au samedi<br/> uniquement",
          sundayToSunday: "Du dimanche au dimanche<br/> uniquement",
          mondayToMonday: "Du lundi au lundi<br/> uniquement",
          minimumRequiredPeriod: "%{minNightInPeriod} %{night} minimum"
        },
        week: "semaine",
        weeks: "semaines"
      },
      periodDates2: [
        {
          endAt: "2022-09-04",
          minimumDuration: 1,
          periodType: "nightly",
          startAt: "2022-09-03"
        },
        {
          endAt: "2023-02-04",
          minimumDuration: 1,
          periodType: "nightly",
          startAt: "2023-02-02"
        },
        {
          endAt: "2023-04-15",
          minimumDuration: 1,
          periodType: "weekly_by_saturday",
          startAt: "2023-02-04"
        }
      ],
      periodDates: [
        {
          startAt: "2022-08-06",
          endAt: "2022-09-10",
          periodType: "weekly_by_saturday",
          minimumDuration: 2
        },
        {
          startAt: "2022-09-10",
          endAt: "2022-10-01",
          periodType: "weekly_by_saturday",
          minimumDuration: 2
        },
        {
          startAt: "2022-10-08",
          endAt: "2022-10-22",
          periodType: "weekly_by_saturday",
          minimumDuration: 2
        },
        {
          startAt: "2022-10-22",
          endAt: "2022-11-26",
          periodType: "weekly_by_saturday",
          minimumDuration: 3
        },
        {
          startAt: "2022-12-18",
          endAt: "2023-01-01",
          periodType: "weekly_by_sunday",
          minimumDuration: 1
        },
        {
          startAt: "2023-01-01",
          endAt: "2023-01-05",
          periodType: "nightly",
          minimumDuration: 3
        },
        {
          startAt: "2023-01-05",
          endAt: "2023-01-15",
          periodType: "nightly",
          minimumDuration: 7
        },
        {
          startAt: "2023-01-15",
          endAt: "2023-01-29",
          periodType: "weekly_by_sunday",
          minimumDuration: 1
        },
        {
          startAt: "2023-01-29",
          endAt: "2023-02-26",
          periodType: "nightly",
          minimumDuration: 10
        },
        {
          startAt: "2023-02-26",
          endAt: "2023-03-05",
          periodType: "weekly_by_sunday",
          minimumDuration: 1
        },
        {
          startAt: "2023-03-11",
          endAt: "2023-04-15",
          periodType: "weekly_by_saturday",
          minimumDuration: 3
        },
        {
          startAt: "2023-04-16",
          endAt: "2023-05-21",
          periodType: "weekly_by_sunday",
          minimumDuration: 1
        },
        {
          startAt: "2023-05-21",
          endAt: "2023-05-25",
          periodType: "nightly",
          minimumDuration: 2
        },
        {
          startAt: "2023-05-25",
          endAt: "2023-05-28",
          periodType: "nightly",
          minimumDuration: 3
        },
        {
          startAt: "2023-05-28",
          endAt: "2023-06-04",
          periodType: "nightly",
          minimumDuration: 7
        },
        {
          startAt: "2023-11-27",
          endAt: "2023-12-25",
          periodType: "weekly_by_monday",
          minimumDuration: 1
        }
      ],
      bookings: [
        {
          id: "1726359",
          checkInDate: "2021-08-22",
          checkOutDate: "2021-08-29",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "1726360",
          checkInDate: "2021-08-15",
          checkOutDate: "2021-08-22",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "1726358",
          checkInDate: "2021-08-01",
          checkOutDate: "2021-08-15",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "1726357",
          checkInDate: "2021-09-01",
          checkOutDate: "2021-09-23",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "1726356",
          checkInDate: "2021-06-01",
          checkOutDate: "2021-06-18",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "181412",
          checkInDate: "2019-09-15",
          checkOutDate: "2019-10-15",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "181491",
          checkInDate: "2019-07-01",
          checkOutDate: "2019-08-31",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "178234",
          checkInDate: "2018-08-04",
          checkOutDate: "2018-08-25",
          style: {
            backgroundColor: "#9DC1C9"
          }
        },
        {
          id: "178235",
          checkInDate: "2018-07-01",
          checkOutDate: "2018-07-31",
          style: {
            backgroundColor: "#9DC1C9"
          }
        }
      ],
      bookings2: [
        {
          id: "3928875",
          triggerEvent: false,
          checkInDate: "2022-09-10",
          checkOutDate: "2022-09-17",
          type: "contract",
          style: { backgroundColor: "#D4A45F" }
        },
        {
          id: "7270382",
          triggerEvent: false,
          checkInDate: "2022-09-17",
          checkOutDate: "2022-09-24",
          type: "contract",
          style: { backgroundColor: "#D4A45F" }
        }
      ],
      newCheckInDate: null,
      newCheckOutDate: null,
      minNights: 3
    };
  },
  computed: {
    dateFormat() {
      return "DD/MM/YYYY";
    },
    lastDateAvailable() {
      return this.addYears(new Date(), 2);
    }
  },
  methods: {
    renderNextMonth() {
      this.dynamicDisabledDates.push(
        "2021-05-11",
        "2021-05-12",
        "2021-05-13",
        "2021-05-14",
        "2021-05-15",
        "2021-05-16",
        "2021-05-17",
        "2021-05-18"
      );
    },
    toggleDatePickerOutside() {
      this.$refs.DatePicker.showDatepicker();
    },
    bookingClicked(event, date, currentBooking) {
      console.log("bookingClicked", event, date, currentBooking);
    },
    periodSelected(event, checkIn, checkOut) {
      console.log("periodSelected", event, checkIn, checkOut);
    },
    handleCheckIncheckOutHalfDay(checkIncheckOutHalfDay) {
      console.log("handleCheckIncheckOutHalfDay", checkIncheckOutHalfDay);
    },
    addYears(dt, n) {
      return new Date(dt.setFullYear(dt.getFullYear() + n));
    },
    validateDateBetweenTwoDates(fromDate, toDate, givenDate) {
      const getvalidDate = d => {
        return new Date(d);
      };

      return (
        getvalidDate(givenDate) <= getvalidDate(toDate) &&
        getvalidDate(givenDate) >= getvalidDate(fromDate)
      );
    },
    dayClicked(date, formatDate, nextDisabledDate) {
      console.log(date, formatDate, nextDisabledDate);
    },
    checkInChanged(newDate) {
      this.newCheckInDate = newDate;
    },
    checkOutChanged(newDate) {
      this.newCheckOutDate = newDate;
    }
  }
};
</script>

<style>
body,
html {
  font-family: "Source Sans Pro", sans-serif;
}

.box {
  width: 100%;
}
.datepicker__fullview .datepicker {
  z-index: 1;
}
</style>
