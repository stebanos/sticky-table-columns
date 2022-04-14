<template>
  <div @click.stop="" class="table-wrap">
    <b-table-simple bordered striped class="gradebook-table">
        <b-thead>
            <b-tr class="table-row table-head-row">
                <b-th class="col-sticky table-student"></b-th>
                <b-th colspan="3" style="background-color: #c2e1e1;border-left: 1px double #c2e1e1">Categorie 1</b-th>
                <b-th colspan="2" style="background-color: #dcead5;">Categorie 2</b-th>
                <b-th class="col-sticky table-student-total"></b-th>
            </b-tr>
            <b-tr class="table-row table-head-row">
                <b-th class="col-sticky table-student">Student</b-th>
                <b-th v-for="fld in fields" :key="fld">{{ metadata[fld].name }}</b-th>
                <b-th class="col-sticky table-student-total">Eindcijfer</b-th>
            </b-tr>
        </b-thead>
        <b-tbody>
            <b-tr v-for="{student, results} in results" :key="student" class="table-row table-body-row">
              <b-td class="col-sticky table-student">{{ student }}</b-td>
              <b-td v-for="fld in fields" :key="fld">{{ results[fld] }}<i class="fa fa-percent" aria-hidden="true"></i><span class="sr-only">%</span></b-td>
              <b-td class="col-sticky table-student-total">20<i class="fa fa-percent" aria-hidden="true"></i><span class="sr-only">%</span></b-td>
            </b-tr>
        </b-tbody>
    </b-table-simple>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

const metadata = {
  'op1': {'name': 'Opdracht 1'},
  'op2': {'name': 'Opdracht 2'},
  'oe1': {'name': 'Oefening 1'},
  'oe2': {'name': 'Oefening 2'},
  'moe': {'name': 'Mondeling examen'}
};

const shownResults = ['op1', 'op2', 'oe1', 'oe2', 'moe'];

const resultsData = [
  { 'student': 'Student 1', 'results': {'op1': 20, 'op2': 60, 'oe1': 80, 'oe2': 50, 'moe': 75} },
  { 'student': 'Student 2', 'results': {'op1': 30, 'op2': 50, 'oe1': 40, 'oe2': 80, 'moe': 65} },
  { 'student': 'Student 3', 'results': {'op1': 50, 'op2': 30, 'oe1': 70, 'oe2': 80, 'moe': 95} },
  { 'student': 'Student 4', 'results': {'op1': 80, 'op2': 40, 'oe1': 40, 'oe2': 30, 'moe': 75} },
  { 'student': 'Student 5', 'results': {'op1': 60, 'op2': 10, 'oe1': 90, 'oe2': 40, 'moe': 25} },
];

@Component({
  name: 'sticky-table',
  components: { }
})
export default class StickyTable extends Vue {
  readonly results = resultsData;
  readonly fields = shownResults;
  readonly metadata = metadata;
}
</script>

<style lang="scss" scoped>
    .table-wrap {
        position: relative;
        overflow-x: auto;
        overflow-y: auto;
    }

    th {
        font-weight: 700;
    }

    .gradebook-table {
        th, td {
            border: 1px solid #ebebeb;
            z-index: 0;
        }

        .table-head-row:first-child th {
            border-bottom: none;
            border-top: 1px solid #ebebeb;

            &:not(:first-child) {
                border-left: none;
            }

            &:not(:last-child) {
                border-right: none;
            }
        }

        .table-head-row:last-child th {
            border-top: none;
        }

        .table-row {
            th, td {
                background-clip: padding-box;

                &:nth-last-child(2) {
                    border-right: none;
                }
            }
        }
    }

    .table-head-row:last-child th {
        background-color: #f8fbfb;
        color: #5885a2;
    }

    .table-body-row:nth-child(even) td {
        background-color: #fff;
    }

    .table-body-row:nth-child(odd) td {
        background-color: #f9f9f9;
    }

    .table-body-row:first-child td {
        background: linear-gradient(to bottom, #e3eaed 0, #f9f9f9 4px);
    }

    .table-row .col-sticky {
        background: linear-gradient(#ebebeb, #ebebeb) no-repeat left/1px 100%, linear-gradient(#ebebeb, #ebebeb) no-repeat right/1px 100%;
        position: sticky;
        z-index: 1;

        &.table-student {
            border-left-color: #fff;
            border-right-color: transparent;
            left: -1px;
        }

        &.table-student-total {
            border-left-color: transparent;
            border-right-color: #fff;
            right: 0;
        }
    }

    @-moz-document url-prefix() {
        .table-row {
            &.table-head-row, &.table-body-row {
                .col-sticky {
                    &.table-student {
                        left: 0;
                    }
                    &.table-student-total {
                        right: -1px;
                    }
                }
            }
        }
    }

    .table-head-row:first-child .col-sticky {
        background-color: #fff;
    }

    .table-body-row:nth-child(even) .col-sticky {
        background-color: #fff;
    }

    .table-body-row:nth-child(odd) .col-sticky {
        background-color: #f9f9f9;
    }

    .table-body-row:first-child .col-sticky {
        background: linear-gradient(#ebebeb, #ebebeb) no-repeat left/1px 100%, linear-gradient(#ebebeb, #ebebeb) no-repeat right/1px 100%,linear-gradient(to bottom, #e3eaed 0, #f9f9f9 4px);
    }

    .fa-percent {
        font-size: 1.1rem;
        margin-left: .15rem;
        opacity: .8;
    }
</style>
