<template>
  <v-container fluid>
    <div class="d-flex flex-row justify-space-between">
      <v-row justify="center">
        <v-col cols="12" md="11">
          <v-card>
            <v-card-title class="headline">
              <div class="d-flex justify-content-center align-items-center mr-2" style="height:50px;width:50px;
              background-color:#E91E63;">
              <v-icon color="white" x-large>help_outline</v-icon>
            </div>
            Q&A
          </v-card-title>
          <v-container fluid>
            <v-row>
              <v-col cols="12" sm="3">
                <v-text-field label="Search" v-model="search" outlined></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <v-divider></v-divider>
          <v-container class="px-4">
            <v-tabs class="">
              <v-tab class="title font-weight-regular mx-4">Inbox</v-tab>
              <v-tab class="title font-weight-regular">Sent</v-tab>
              <v-tab-item>
                <v-list two-line>
                  <v-list-item-group>
                    <template v-for="(item, index) in items">
                      <v-list-item :key="item.title">
                        <template>
                          <v-list-item-avatar>
                            <v-icon x-large color="#E91E63">mdi-alpha-{{item.title.charAt(0).toLowerCase()}}-circle</v-icon>
                          </v-list-item-avatar>
                          <v-list-item-content @click="inboxDialog = true">
                            <v-list-item-title v-text="item.title"></v-list-item-title>
                            <v-list-item-subtitle class="text--primary" v-text="item.headline"></v-list-item-subtitle>
                            <v-list-item-subtitle v-text="item.subtitle"></v-list-item-subtitle>
                          </v-list-item-content>

                          <v-list-item-action>
                            <v-list-item-action-text v-text="item.action"></v-list-item-action-text>
                          </v-list-item-action>
                        </template>
                      </v-list-item>

                      <v-divider v-if="index < items.length" :key="index"></v-divider>
                    </template>
                  </v-list-item-group>
                </v-list>

              </v-tab-item>
              <v-tab-item>
                <v-list two-line>
                  <v-list-item-group>
                    <template v-for="(item, index) in items">
                      <v-list-item :key="item.title">
                        <template>
                          <v-list-item-avatar>
                            <v-icon x-large color="#E91E63">mdi-alpha-{{item.title.charAt(0).toLowerCase()}}-circle</v-icon>
                          </v-list-item-avatar>
                          <v-list-item-content @click="sentDialog = true">
                            <v-list-item-title v-text="item.title"></v-list-item-title>
                            <v-list-item-subtitle class="text--primary" v-text="item.headline"></v-list-item-subtitle>
                            <v-list-item-subtitle v-text="item.subtitle"></v-list-item-subtitle>
                          </v-list-item-content>

                          <v-list-item-action>
                            <v-list-item-action-text v-text="item.action"></v-list-item-action-text>
                          </v-list-item-action>
                        </template>
                      </v-list-item>

                      <v-divider v-if="index < items.length" :key="index"></v-divider>
                    </template>
                  </v-list-item-group>
                </v-list>

              </v-tab-item>
            </v-tabs>
          </v-container>

        </v-card>
      </v-col>
    </v-row>

    <div class="float-right button-container">
      <div class="buttons">
        <v-row class="ma-2 mb-4">
          <button class="float-right ml-2 v-btn v-btn--depressed theme--light" style="background-color:#E91E63" icon>
            <v-icon color="white" x-large>question_answer</v-icon>
          </button>
        </v-row>
      </div>
    </div>

    <v-dialog v-model="writeDialog" max-width="1000" max-height="500">
      <v-card>
        <v-card-title class="headline">
          <div class="d-flex justify-content-center align-items-center mr-2" style="height:50px;width:50px;
          background-color:#E91E63;">
          <v-icon color="white" x-large>help_outline</v-icon>
        </div>
        Q&A
      </v-card-title>
      <v-container fluid>
        <v-row>
          <v-col cols="12" sm="3">
            <v-select v-model="category" label="Category" :items="categories"></v-select>
          </v-col>
          <v-col cols="12" sm="9">
            <v-text-field v-model="subject" label="Subject"></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12">
            <v-textarea filled placeholder="Write here ..." v-model="writeText"></v-textarea>
          </v-col>
        </v-row>
        <v-row class="d-flex justify-content-end">
          <v-btn text style="color:#E91E63" @click="writeDialog = false">Cancel</v-btn>
          <v-btn color="#E91E63" class="white--text mx-2">Submit</v-btn>
        </v-row>
      </v-container>
    </v-card>
  </v-dialog>

  <v-dialog v-model="inboxDialog" max-width="1000" max-height="500">
    <v-card>
      <v-card-title class="headline">
        <div class="d-flex justify-content-center align-items-center mr-2" style="height:50px;width:50px;
        background-color:#E91E63;">
        <v-icon color="white" x-large>help_outline</v-icon>
      </div>
      Q&A
    </v-card-title>
    <v-container fluid>
      <v-row>
        <v-col cols="12" sm="3">
          <p class="title font-weight-regular">Student Name</p>
        </v-col>
        <v-col cols="12" sm="9">
          <p class="title font-weight-regular">Re: [Subject]</p>
        </v-col>
      </v-row>
      <v-divider class="mt-0"></v-divider>
      <v-row>
        <v-col cols="12">
          <p class="subtitle-1 font-weight-regular black--text">Lorem ipsum dolor sit amet, integer sed eros urna, ipsum fermentum cursus sit massa nullam et, ut et elit at. Ultrices eleifend scelerisque. Molestie at massa morbi ullamcorper, sit duis,
            lacus non magna, ante quam, non augue sit est. Neque urna justo conubia congue vitae, mauris et amet augue urna diam. Curabitur massa elit, fringilla dolore posuere venenatis, curabitur etiam imperdiet non eu integer, mauris nullam et dolor.
            Blandit ullamcorper, vel consectetuer turpis mauris, vel enim donec, id leo leo urna facilisi. Imperdiet laoreet tempor cubilia amet, adipiscing condimentum, diam consectetuer, amet in neque dolor dui pellentesque, diam lacus risus lacinia
            quis vitae.</p>
          </v-col>
          <v-col cols="12" class="pt-0">
            <v-divider class="mt-0"></v-divider>
            <v-textarea filled></v-textarea>
            </v-col>
        </v-row>
        <v-row class="d-flex justify-content-end">
          <v-btn text style="color:#1976d2" class="mx-2" @click="inboxDialog = false">Close</v-btn>
          <v-btn color="#E91E63" class="white--text mx-2">Reply</v-btn>
        </v-row>
      </v-container>
    </v-card>
  </v-dialog>

  <v-dialog v-model="sentDialog" max-width="1000" max-height="500">
    <v-card>
      <v-card-title class="headline">
        <div class="d-flex justify-content-center align-items-center mr-2" style="height:50px;width:50px;
        background-color:#E91E63;">
        <v-icon color="white" x-large>help_outline</v-icon>
      </div>
      Write
    </v-card-title>
    <v-container fluid>
      <v-row>
        <v-col cols="12" sm="3">
          <p class="title font-weight-regular">Category</p>
        </v-col>
        <v-col cols="12" sm="9">
          <p class="title font-weight-regular">Re: [Subject]</p>
        </v-col>
      </v-row>
      <v-divider class="mt-0"></v-divider>
      <v-row>
        <v-col cols="12">
          <p class="subtitle-1 font-weight-regular">Lorem ipsum dolor sit amet, integer sed eros urna, ipsum fermentum cursus sit massa nullam et, ut et elit at. Ultrices eleifend scelerisque. Molestie at massa morbi ullamcorper, sit duis, lacus non
            magna, ante quam, non augue sit est. Neque urna justo conubia congue vitae, mauris et amet augue urna diam. Curabitur massa elit, fringilla dolore posuere venenatis, curabitur etiam imperdiet non eu integer, mauris nullam et dolor. Blandit
            ullamcorper, vel consectetuer turpis mauris, vel enim donec, id leo leo urna facilisi. Imperdiet laoreet tempor cubilia amet, adipiscing condimentum, diam consectetuer, amet in neque dolor dui pellentesque, diam lacus risus lacinia quis
            vitae.</p>
          </v-col>
        </v-row>
        <v-row class="d-flex justify-content-end">
          <v-btn color="#E91E63" class="white--text mx-2" @click="sentDialog = false">Close</v-btn>
        </v-row>
      </v-container>
    </v-card>
  </v-dialog>

</div>
</v-container>
</template>

<script>
export default {
  data: () => ({
    selected: [2],
    writeDialog: false,
    inboxDialog: false,
    sentDialog: false,

    categories: ['Technical Issue', 'Class Issue', 'Schedule Issue', 'Account Issue'],

    items: [{
      action: '15 min',
      headline: 'Brunch this weekend?',
      title: 'Ali Connors',
      subtitle: "I'll be in your neighborhood doing errands this weekend. Do you want to hang out?",
    },
    {
      action: '2 hr',
      headline: 'Summer BBQ',
      title: 'me, Scrott, Jennifer',
      subtitle: "Wish I could come, but I'm out of town this weekend.",
    },
    {
      action: '6 hr',
      headline: 'Oui oui',
      title: 'Sandra Adams',
      subtitle: 'Do you have Paris recommendations? Have you ever been?',
    },
    {
      action: '12 hr',
      headline: 'Birthday gift',
      title: 'Trevor Hansen',
      subtitle: 'Have any ideas about what we should get Heidi for her birthday?',
    },
    {
      action: '18hr',
      headline: 'Recipe to try',
      title: 'Britta Holt',
      subtitle: 'We should eat this: Grate, Squash, Corn, and tomatillo Tacos.',
    },
  ],
}),
}
</script>

<style lang="css">

.button-container {
  width: 50px;
  position: relative;
}

.buttons {
  margin: 0;
  position: absolute;
  top: 50%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
}

</style>
