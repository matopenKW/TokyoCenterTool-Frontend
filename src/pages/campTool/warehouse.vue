<template>
    <div id="warehouse">
        <h2> 倉庫 / 資材</h2>
        <div id="warehouse-search-area" class="row">
            <div class="col-12">
                検索機能 Comming Soon...
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'

export default {
    
}
</script>

<style>

#warehouse h2 {
    margin-bottom: 2vh;
}

#warehouse #warehouse-search-area {
    margin-bottom: 2vh;
    height: 50px;
    background-color: #eee;
    border: 1px solid #bbb;
}

#warehouse #warehouse-search-area > div {
    margin: auto;
}

#warehouse #warehouse-search-area {
    margin-bottom: 2vh;
}

#warehouse #warehouse-search-area > div {
    margin: auto;
}

#warehouse #warehouse-search-area {
    justify-content: center;
}

#warehouse #warehouse-search-area .btn {
    width: 76px;
}

#warehouse #warehouse-search-area .carfareList:checked {
    background-color: red;
}

</style>