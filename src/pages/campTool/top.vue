<template>
    <div id="top">
        <div class="row">
            <div id="carfare" class="app col-xs-12 col-sm-4 text-center" @click="clickCarfare">
                <div class="title">交通費管理</div>
                <div class="icon">
                    <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="subway" class="svg-inline--fa fa-subway fa-w-14" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M448 96v256c0 51.815-61.624 96-130.022 96l62.98 49.721C386.905 502.417 383.562 512 376 512H72c-7.578 0-10.892-9.594-4.957-14.279L130.022 448C61.82 448 0 403.954 0 352V96C0 42.981 64 0 128 0h192c65 0 128 42.981 128 96zM200 232V120c0-13.255-10.745-24-24-24H72c-13.255 0-24 10.745-24 24v112c0 13.255 10.745 24 24 24h104c13.255 0 24-10.745 24-24zm200 0V120c0-13.255-10.745-24-24-24H272c-13.255 0-24 10.745-24 24v112c0 13.255 10.745 24 24 24h104c13.255 0 24-10.745 24-24zm-48 56c-26.51 0-48 21.49-48 48s21.49 48 48 48 48-21.49 48-48-21.49-48-48-48zm-256 0c-26.51 0-48 21.49-48 48s21.49 48 48 48 48-21.49 48-48-21.49-48-48-48z"></path></svg>
                </div>
            </div>
            <div id="warehouse" class="app col-xs-12 col-sm-4 text-center" @click="clickWarehouse">
                <div class="title">倉庫・資材</div>
                <div class="icon">
                    <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="wrench" class="svg-inline--fa fa-wrench fa-w-16" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M507.73 109.1c-2.24-9.03-13.54-12.09-20.12-5.51l-74.36 74.36-67.88-11.31-11.31-67.88 74.36-74.36c6.62-6.62 3.43-17.9-5.66-20.16-47.38-11.74-99.55.91-136.58 37.93-39.64 39.64-50.55 97.1-34.05 147.2L18.74 402.76c-24.99 24.99-24.99 65.51 0 90.5 24.99 24.99 65.51 24.99 90.5 0l213.21-213.21c50.12 16.71 107.47 5.68 147.37-34.22 37.07-37.07 49.7-89.32 37.91-136.73zM64 472c-13.25 0-24-10.75-24-24 0-13.26 10.75-24 24-24s24 10.74 24 24c0 13.25-10.75 24-24 24z"></path></svg>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        async clickCarfare(){
            window.location.href = './carfare'
        },
        async clickWarehouse(){
            window.location.href = './warehouse'
        }
    }
}
</script>

<style>
.row {
    margin: 0 3vh;
}
.app {
    margin: 0 1vw;
    margin-bottom: 5.5vh;
    box-shadow: 0 3px 5px rgba(0, 0, 0, 0.22);
    height: 450px;
    cursor: pointer;
    
}

.app .title {
    font-size: 2.5vh;
    margin: 2vh 0;
}

.app .icon {
    height: 80%;
    background: #e9ecef;
    vertical-align: middle;
    display: flex;
    align-items: center;
	justify-content: center;

}

.app .icon svg {
    height: 150px;
}


</style>