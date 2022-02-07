<template>
<div class="container">
    <div class="row">
        <div class="col-12">
            <div>
                <i class="fas fa-spinner"></i>
            </div>
        </div>
    </div>    
</div>
</template>

<script>
export default {
    name: 'LoadingWait',

}
</script>

<style lang="scss" scoped>
.col-12 {
    display: flex;
    justify-content: center;
    font-size: 100px;
    div {
        animation-name: spin;
        animation-duration: 4s;
        animation-iteration-count: infinite;
        animation-timing-function: linear;
    }
}

@keyframes spin {
  0%   {transform: rotate(0deg);}
  25%  {transform: rotate(90deg);}
  50%  {transform: rotate(180deg);}
  75%  {transform: rotate(270deg);}
  100% {transform: rotate(360deg);}
}

</style>