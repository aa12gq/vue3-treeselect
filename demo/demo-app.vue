<template>

  <div>
    <vue-treeselect multiple  v-model="selected" :options="treeData"
                    noResultsText="No results..."
                    placeholder="Select items..."
    >

    </vue-treeselect>
    <div>
      Selected: {{ selected }}
    </div>
  </div>
</template>
<script>
import {defineComponent, ref, reactive} from 'vue';
import {ASYNC_SEARCH} from '../src/';

export default defineComponent({

  setup() {
    const loadOptions = ({action, searchQuery, callback}) => {
      if (action === ASYNC_SEARCH) {
        setTimeout(() => {
          const options = [1, 2, 3, 4, 5].map(i => ({
            id: `${searchQuery}-${i}`,
            label: `${searchQuery}-${i}`,
          }))
          console.log(options);
          callback(null, options)
        }, 2000);
      }
    }
    let selected = ref([7, 8]);
    let treeOrientation = ref("0");
    let treeData = ref(
        [
          {label: '<span style="color: brown">child 1</span>', id: 2,},
          {label: 'child 2', id: 3,},
          {
            label: 'subparent 1',
            id: 4,
            expand: false,
            children: [
              {label: 'subchild 1', id: 5},
              {
                label: 'subchild 2',
                id: 6,
                expand: false,
                children: [
                  {label: 'subchild 11', id: 7},
                  {label: 'subchild 22', id: 8},
                ]
              },
            ]
          },
        ]
    );


    return {
      treeData,
      selected,
      loadOptions
    }
  }
})

</script>
