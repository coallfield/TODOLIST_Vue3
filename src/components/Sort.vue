<template>
    <div class="sort">
        <SortButton @click="getSorted" class="big-suc" id="succ" :class="{ 'active-sort': currentSort === 'succ' }">Successed</SortButton >
                <SortButton @click="getSorted" style="display: none;" class="small-suc" id="succ" :class="{ 'active-sort': currentSort === 'succ' }">✔</SortButton >

        <SortButton @click="getSorted" id="all" :class="{ 'active-sort': currentSort === 'all' || !currentSort }">All</SortButton >

        <SortButton @click="getSorted" class="big-unsuc" id="unsucc" :class="{ 'active-sort': currentSort === 'unsucc' }" >Unsuccessed</SortButton >
                <SortButton @click="getSorted" style="display: none;" class="small-unsuc" id="unsucc" :class="{ 'active-sort': currentSort === 'unsucc' }">‒</SortButton >
    </div>
</template>

<script>
export default {
    props: {
        currentSort: {
            type: String
        }
    },
    methods: {
        getSorted(event) {
            this.$emit('update:currentSort', event.target.id)
        }
    }   
}
</script>

<style scoped>
.sort {

  display: flex;
  margin-left: auto;
  margin-right: auto;
  width: 900px;
  justify-content: center;
  margin-top: 15px;
  grid-gap: 160px;
  
}

</style>