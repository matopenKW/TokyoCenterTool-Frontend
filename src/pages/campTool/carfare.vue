<template>
    <div id="carfare">
        <h2>交通費管理</h2>
        <div id="carfare-search-area" class="row">
            <div class="col-12">
                検索機能 Comming Soon...
            </div>
        </div>
        <div id="carfare-action-area" class="row">
            <div class="col-12">
                <input type="button" class="btn btn-primary" value="追加" @click="clickAddRow(index)">
                <input type="button" class="btn btn-primary" value="コピー" @click="clickRegistBtn(index)">
            </div>
        </div>
        <div id="carfare-list-area" class="row">
            <table>
                <thead>
                    <tr>
                        <td class="date-head">日付</td>
                        <th class="route-head" scope="col">内容</th>
                        <th class="price-head" scope="col">料金</th>
                        <th class="btn-area-head" scope="col"></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(carfare, index) in carfareList" :key="carfare.SeqNo" class="carfareList" @click="clickRow(index)">
                        <th class="date" @click="clickDate(index)">
                            <span v-if="selectDateIndex == index">
                                <input type="text" v-model="carfare.Date">
                            </span>
                            <span v-else>
                                {{ carfare.Date | format-date }}
                            </span>
                        </th>
                        <td v-show="verticalMode || selectIndex == index" data-label="内容" class="route">
                            <div class="row">
                                <div class="col-md-12 col-lg-5">
                                    <input type="text" v-model="carfare.StartPoint">
                                </div>
                                <div class="arrow text-center col-md-12 col-lg-1"></div>
                                <div class="col-md-12 col-lg-5">
                                    <input type="text" v-model="carfare.EndPoint">
                                </div>
                            </div>
                        </td>
                        <td v-show="verticalMode || selectIndex == index" data-label="価格" class="price">
                            <input type="text" v-model="carfare.Price">
                        </td>
                        <td v-show="verticalMode || selectIndex == index" data-label="" class="btn-area">
                            <span v-if="carfare.isNewRow">
                                <input type="button" class="btn btn-primary" value="登録" @click="clickRegistBtn(index)">
                            </span>
                            <span v-else>
                                <input type="button" class="btn btn-success" value="更新" @click="clickUpdateBtn(index)">
                            </span>
                            <input type="button" class="btn btn-danger" value="削除" @click="clickDeleteBtn(index)">
                        </td>
                    </tr>
                </tbody>
            </table>   
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'

export default {
    data: function(){
        return {
            carfareList: [],
            verticalMode: true,
            selectIndex: 0,
            selectDateIndex: -1
        }
    },
    methods: {
        handleResize: function(){
            this.verticalMode = window.innerWidth > 768
        },
        async clickAddRow(){
            let sysDate = this.$moment(new Date())
            this.carfareList.push({
                    Date: sysDate.format('YYYYMMDD'),
                    StartPoint: '',
                    EndPoint: '',
                    Price: 0,
                    isNewRow: true
            })
        },
        async clickRow(index){
            this.selectIndex = index
        },
        async clickDate(index){
            this.selectDateIndex = index
        },
        async clickUpdateBtn(index){
            let carfare = this.carfareList[index]
            this.$axios.$get('/carfare/update',{
                params: carfare
            }).then(response => {
                alert('更新しました。')
            })
            .catch(err => {
                alert('更新に失敗しました。')
                console.log(err)
            })
        },
        async clickRegistBtn(index){
            let carfare = this.carfareList[index]

            this.$axios.$get('/carfare/regist',{
                params: carfare
            }).then(response => {
                alert('登録しました。')
                carfare.isNewRow = false
                carfare.SeqNo = response.SeqNo
            })
            .catch(err => {
                alert('登録に失敗しました。')
                console.log(err)
            })
        },
        async clickDeleteBtn(index){

            let carfare = this.carfareList[index]
            if (!carfare.isNewRow) {
                this.$axios.$get('/carfare/delete',{
                    params: carfare
                }).then(response => {
                    alert('削除しました。')
                    this.carfareList.splice(index, 1)
                })
                .catch(err => {
                    alert('削除に失敗しました。')
                    console.log(err)
                })
            }　else {
                this.carfareList.splice(index, 1)
            }

        }
    },
    mounted: function(){
        this.verticalMode = window.innerWidth > 768
        window.addEventListener('resize', this.handleResize)

        this.$nextTick(function () {
            this.$axios.$get('/carfare/select',{
                params:{}
            })
            .then(response => {
                this.carfareList = response
                this.carfareList.forEach(element => {
                    element.isNewRow = false
                });
            })
            .catch(err => {
                alert('データの取得に失敗しました。')
                console.log(err)
            })
        })
    }
}
</script>

<style>

#carfare h2 {
    margin-bottom: 2vh;
}

#carfare #carfare-search-area {
    margin-bottom: 2vh;
    height: 50px;
    background-color: #eee;
    border: 1px solid #bbb;
}

#carfare #carfare-search-area > div {
    margin: auto;
}

#carfare #carfare-action-area {
    margin-bottom: 2vh;
}

#carfare #carfare-action-area > div {
    margin: auto;
}

#carfare #carfare-list-area {
    justify-content: center;
}

#carfare #carfare-list-area .btn {
    width: 76px;
}

#carfare #carfare-list-area .carfareList:checked {
    background-color: red;

}

/*テーブルレイアウト */
table .date-head {
    font-size: .85em;
    width: 130px;
}

table .price-head {
    width: 110px;
}

table .btn-area-head {
    width: 200px;
}

table .date input {
    width: 90px;
}

table .route input{
    width: 100%;
}

table .route .arrow:after {
    content: '→';
}

table .price input {
    width: 75px;
    text-align: right;
}

@media screen and (max-width: 992px) {
    table .route .arrow:after {
        content: '↓';
    }
}

/*テーブルレイアウト defalt*/
table {
  border-collapse: collapse;
  margin: 0 auto;
  padding: 0;
  width: 100%;
  table-layout: fixed;
}

table tr {
  background-color: #fff;
  border: 1px solid #bbb;
  padding: .35em;
}
table th,
table td {
  padding: 1em 10px 1em 1em;
  border-right: 1px solid #bbb;
}
table th {
  font-size: .85em;
}
table thead tr{
  background-color: #eee;
}
table .route{
   text-align: left;
   font-size: .85em;
}
table .price{
   text-align: right;
}
@media screen and (max-width: 768px) {

  table {
    border: 0;
    width:100%
  }
  table th{
    background-color: #eee;
    display: block;
    border-right: none;
  }
  table thead {
    border: none;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
  }
  
  table tr {
    display: block;
    margin-bottom: .625em;
  }
  
  table td {
    border-bottom: 1px solid #bbb;
    display: block;
    font-size: .8em;
    text-align: right;
    position: relative;
    padding: .625em .625em .625em 4em;
    border-right: none;
  }
  
  table td::before {
    content: attr(data-label);
    font-weight: bold;
    position: absolute;
    left: 10px;
  }
  
  table td:last-child {
    border-bottom: 0;
  }
}
</style>