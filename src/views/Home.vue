<template>
  <v-app>
    <!-- giving the template background -->
    <v-main style="background:#262a41">
      <!-- creating rows and columns for the search and All Users -->
      <v-row no-gutters>
        <v-col cols="12" sm="12" md="12" lg="6">
          <!-- Hello,Emerald and the search bar -->
          <div style="margin:100px;margin-top:230px">
            <p class="white--text font-weight-thin" style="font-size:30px">
              Hello, <span class="white--text font-weight-black">Emerald</span>
            </p>
            <p class="font-weight-thin white--text" style="font-size:12px">
              Welcome to your dashboard, kindly sort through the user base
            </p>
            <v-text-field
              v-model="search"
              height="60px"
              elevation="24"
              color="#3c3f54"
              label="Find a user"
              solo
              prepend-inner-icon="mdi-magnify"
              style="border-radius:15px;opacity:0.4"
            />

            <p style="margin-top:20px;color:white;font-size:14px">Show Users</p>
            <div style="margin-left:-20px">
              <!-- The All Users, Male users and female users -->
              <v-row>
                <v-col>
                  <v-card
                    class="mx-6 text-center elevation-24"
                    color="#f935a9"
                    style="padding:24px;border-radius:20px"
                    @click="refresh"
                  >
                    <v-icon large class="white--text">
                      mdi-account-group</v-icon
                    >
                  </v-card>
                  <p
                    class="font-weight-thin white--text"
                    style="font-size:12px;text-align:center;margin-top:14px"
                  >
                    All users
                  </p>
                </v-col>
                <v-col order="2">
                  <v-card
                    class="mx-6 text-center elevation-24"
                    color="#30bbb5"
                    style="padding:24px;border-radius:20px"
                    @click="forMale"
                  >
                    <v-icon large class="white--text"> mdi-human-male</v-icon>
                  </v-card>
                  <p
                    class="font-weight-thin white--text"
                    style="font-size:12px;text-align:center;margin-top:14px"
                  >
                    Male users
                  </p>
                </v-col>
                <v-col order="3">
                  <v-card
                    class="mx-6 text-center elevation-24"
                    color="#7946c1"
                    style="padding:24px;border-radius:20px; margin-right:-20px;padding-right:-30px"
                    @click="forFemale"
                  >
                    <v-icon large class="white--text"> mdi-human-female</v-icon>
                  </v-card>
                  <p
                    class="font-weight-thin white--text"
                    style="font-size:12px;text-align:center;margin-top:14px"
                  >
                    Female users
                  </p>
                </v-col>
              </v-row>
            </div>
          </div>
        </v-col>
        <!-- The All Users Column -->
        <v-col cols="12" sm="12" md="12" lg="6">
          <v-card
            width="5000"
            class="hidden-md-and-down"
            style="margin-top:120px;border-radius:17px;margin-left:-40px;margin-right:-700px;padding-right:-300px;padding-bottom:60px"
            color="#f7f7ff"
          >
            <!-- Creating a window view to move from All Users to User List -->
            <v-window v-model="step">
              <v-window-item :value="1">
                <div style="padding-top:50px;margin:30px">
                  <h3
                    class="font-weight-bold"
                    style="color:#30344a;font-size:22px"
                  >
                    All Users
                  </h3>
                  <p style="font-size:12px">Filter by</p>

                  <v-row>
                    <v-col cols="8" sm="5" md="5">
                      <v-text-field
                        v-model="search"
                        rounded
                        color="#e2e3ec"
                        label="Find in list"
                        filled
                        prepend-inner-icon="mdi-magnify"
                      />
                    </v-col>
                    <v-col order="1" cols="6" sm="4" md="4">
                      <v-select
                        :items="items"
                        label="Country"
                        dense
                        filled
                        rounded
                      ></v-select>
                    </v-col>
                    <v-col order="2" cols="4" sm="3" md="3">
                      <v-switch
                        v-model="switch1"
                        color="#30bbb5"
                        label="Show Country"
                        style="padding-right:20px;font-size:12px;margin-top:-2px"
                        class="mx-3"
                      ></v-switch>
                    </v-col>
                  </v-row>

                  <div v-for="(person, i) in people" :key="i">
                    <v-card
                      class="pa-5 elevation-24"
                      style="border-radius:10px;margin-bottom:30px"
                    >
                      <v-row>
                        <v-col cols="6" md="2" sm="5">
                          <v-avatar size="100px">
                            <v-img
                              :src="person.picture.large"
                              style="border-radius:60px;border:solid;border-color:#75d6d1;border-width:6px"
                            />
                          </v-avatar>
                        </v-col>
                        <v-col cols="10" md="10" sm="7">
                          <p
                            style="margin:7px;font-size:20px;padding-left:30px"
                            class="font-weight-bold"
                          >
                            {{ person.name.first }} {{ person.name.last }}
                          </p>
                          <p
                            style="padding-left:40px;font-size:15px"
                            class="font-weight-bold font-italic"
                          >
                            {{ person.location.street.number }},
                            {{ person.location.city }},
                            {{ person.location.state }}
                          </p>
                          <div style="padding-left:22px;margin-top:-30px">
                            <v-row>
                              <v-col cols="12" md="6" sm="5">
                                <v-btn
                                  color="#f7d9f2"
                                  depressed
                                  text
                                  style="margin-top:23px;border-radius:40px"
                                  ><v-icon color="#BABDD1"
                                    >mdi-email-outline</v-icon
                                  ><span
                                    style="opacity:0.6;color:#262A41;text-align:center;font-size:12px"
                                  >
                                    {{ person.email }}
                                  </span></v-btn
                                >
                              </v-col>

                              <v-col cols="12" md="4" sm="5">
                                <v-btn
                                  color="#f7d9f2"
                                  depressed
                                  text
                                  style="margin-top:23px;border-radius:40px"
                                  ><v-icon color="#BABDD1"
                                    >mdi-phone-in-talk-outline</v-icon
                                  ><span
                                    style="opacity:0.6;color:#262A41;text-align:center;font-size:12px"
                                  >
                                    {{ person.phone }}
                                  </span></v-btn
                                >
                              </v-col>

                              <v-col cols="12" md="2" sm="2">
                                <v-btn
                                  width="50px"
                                  height="50px"
                                  @click="goNext(i)"
                                  style="border-radius:14px;margin-top:8px"
                                  class="elevation-24 pa-3"
                                  color="#75d6d1"
                                >
                                  <v-icon class="white--text" medium>
                                    mdi-arrow-right
                                  </v-icon></v-btn
                                >
                              </v-col>
                            </v-row>
                          </div>
                        </v-col>
                      </v-row>
                    </v-card>
                  </div>
                </div>
                <!-- Download Results and the back and forward buttons -->
                <v-row>
                  <v-col>
                    <div style="margin-left:30px">
                      <v-btn
                        rounded
                        height="50px"
                        color="#7946c1"
                        class="white--text"
                      >
                        <v-icon class="px-2">mdi-cloud-download-outline</v-icon
                        >Download Results</v-btn
                      >
                    </div>
                  </v-col>

                  <v-col>
                    <div style="margin-left:170px;margin-top:10px">
                      <v-btn
                        color="#e2e3ec"
                        small
                        height="40px"
                        width="25px"
                        style="border-radius:10px"
                        ><v-icon color="#262a41"
                          >mdi-chevron-left</v-icon
                        ></v-btn
                      ><v-btn
                        class="mx-2"
                        color="#262a41"
                        style="border-radius:10px"
                        small
                        height="40px"
                        width="25px"
                        ><v-icon class="white--text"
                          >mdi-chevron-right</v-icon
                        ></v-btn
                      >
                    </div>
                  </v-col>
                </v-row>
              </v-window-item>

              <v-window-item :value="2">
                <div style="padding-top:50px;margin:50px;text-align:left">
                  <h3
                    class="font-weight-bold"
                    style="color:#30344a;font-size:22px"
                  >
                    User List
                  </h3>
                  <p style="font-size:12px">Filter by</p>

                  <v-row justify-start>
                    <v-col cols="8" sm="8" md="8" lg="5">
                      <v-text-field
                        v-model="search"
                        rounded
                        color="#e2e3ec"
                        label="Find in list"
                        filled
                        prepend-inner-icon="mdi-magnify"
                      />
                    </v-col>
                    <v-col order="1" cols="6" sm="4" md="4">
                      <v-select
                        :items="items"
                        label="Country"
                        dense
                        filled
                        rounded
                      ></v-select>
                    </v-col>
                    <v-col order="2" cols="4" sm="3" md="3">
                      <v-switch
                        v-model="switch1"
                        color="#30bbb5"
                        label="Show Country"
                        style="padding-right:20px;font-size:12px;margin-top:-2px"
                        class="mx-3"
                      ></v-switch>
                    </v-col>
                  </v-row>

                  <v-btn text @click="goBack">
                    <v-icon color="#75d6d1" style="margin-right:10px"
                      >mdi-arrow-left</v-icon
                    >RESULTS</v-btn
                  >

                  <div v-for="(person, i) in onePerson" :key="i">
                    <v-row>
                      <v-col cols="6" md="3" sm="6">
                        <v-avatar size="200px" class="my-3">
                          <v-img
                            :src="person.picture.large"
                            style="border-radius:200px;border:solid;border-color:#75d6d1;border-width:6px"
                          />
                        </v-avatar>
                      </v-col>
                      <v-col cols="9" md="9" sm="6">
                        <p
                          style="margin-top:20px;font-size:23px;padding-left:80px;color:#30344a"
                          class="font-weight-black"
                        >
                          {{ person.name.title }} {{ person.name.first }}
                          {{ person.name.last
                          }}<span class="font-weight-light ml-2">{{
                            person.dob.age
                          }}</span>
                        </p>
                        <p
                          style="padding-left:80px;font-size:15px;margin-top:-7px"
                        >
                          {{ person.location.street.number }},
                          {{ person.location.city }},
                          {{ person.location.state }}
                        </p>

                        <div style="padding-left:80px">
                          <v-btn rounded color="#e2e3ec" disabled
                            ><v-icon>mdi-email-outline</v-icon
                            ><span style="color:#262A41;padding-left:3px"
                              >{{ person.email }}
                            </span></v-btn
                          >
                          <v-btn
                            color="#f7d9f2"
                            depressed
                            style="margin-top:23px;border-radius:40px;text-align:center"
                            ><span
                              style="opacity:1;color:#262A41;text-align:center;font-size:12px"
                              >JOINED: {{ person.registered.date }}
                            </span></v-btn
                          >
                          <v-btn
                            color="#f7d9f2"
                            depressed
                            text
                            style="margin-left:-8px;margin-top:23px;border-radius:40px;text-align:center"
                            ><v-icon color="#BABDD1"
                              >mdi-phone-in-talk-outline</v-icon
                            ><span
                              style="opacity:1;color:#BABDD1;text-align:center;font-size:12px"
                            >
                              {{ person.phone }}
                            </span></v-btn
                          >
                          <div style="margin-top:-20px">
                            <v-btn
                              color="#f7d9f2"
                              depressed
                              text
                              style="margin-left:-8px;margin-top:23px;border-radius:40px;text-align:center"
                              ><v-icon color="#BABDD1"
                                >mdi-cellphone-iphone</v-icon
                              ><span
                                style="opacity:1;color:#BABDD1;text-align:center;font-size:12px"
                              >
                                {{ person.cell }}
                              </span></v-btn
                            >
                          </div>
                        </div>
                      </v-col>
                    </v-row>
                  </div>
                </div>

                <v-row>
                  <v-col>
                    <div style="margin-left:30px">
                      <v-btn
                        rounded
                        height="50px"
                        color="#7946c1"
                        class="white--text"
                        style="opacity:0.3"
                      >
                        <v-icon class="px-2">mdi-cloud-download-outline</v-icon
                        >Download Results</v-btn
                      >
                    </div>
                  </v-col>

                  <v-col>
                    <div style="margin-left:170px;margin-top:10px">
                      <v-btn
                        color="#e2e3ec"
                        small
                        height="40px"
                        width="25px"
                        style="border-radius:10px;opacity:0.3"
                        ><v-icon color="#262a41"
                          >mdi-chevron-left</v-icon
                        ></v-btn
                      ><v-btn
                        class="mx-2"
                        color="#262a41"
                        style="border-radius:10px;opacity:0.3"
                        small
                        height="40px"
                        width="25px"
                        ><v-icon class="white--text"
                          >mdi-chevron-right</v-icon
                        ></v-btn
                      >
                    </div>
                  </v-col>
                </v-row>
              </v-window-item>
            </v-window>
          </v-card>
          <!-- Mobile view of All Users, for responsiveness -->
          <div class="hidden-lg-and-up" style="text-align:center">
            <v-card
              width="5000"
              justify-center
              style="margin-top:120px;border-radius:17px;padding-bottom:60px"
              color="#f7f7ff"
            >
              <v-window v-model="step">
                <v-window-item :value="1">
                  <div style="padding-top:50px;margin:30px">
                    <h3
                      class="font-weight-bold"
                      style="color:#30344a;font-size:22px"
                    >
                      All Users
                    </h3>
                    <p style="font-size:12px">Filter by</p>

                    <v-row>
                      <v-col cols="8" sm="5" md="5">
                        <v-text-field
                          v-model="search"
                          rounded
                          color="#e2e3ec"
                          label="Find in list"
                          filled
                          prepend-inner-icon="mdi-magnify"
                        />
                      </v-col>
                      <v-col order="1" cols="6" sm="4" md="4">
                        <v-select
                          :items="items"
                          label="Country"
                          dense
                          filled
                          rounded
                        ></v-select>
                      </v-col>
                      <v-col order="2" cols="4" sm="3" md="3">
                        <v-switch
                          v-model="switch1"
                          color="#30bbb5"
                          label="Show Country"
                          style="padding-right:20px;font-size:12px;margin-top:-2px"
                          class="mx-3"
                        ></v-switch>
                      </v-col>
                    </v-row>

                    <div v-for="(person, i) in people" :key="i">
                      <v-card
                        class="pa-5 elevation-24"
                        style="border-radius:10px;margin-bottom:30px;text-align:center"
                      >
                        <v-row>
                          <v-col cols="6" md="2" sm="6">
                            <v-avatar size="100px" style="margin-left:92px">
                              <v-img
                                :src="person.picture.large"
                                style="border-radius:60px;border:solid;border-color:#75d6d1;border-width:6px"
                              />
                            </v-avatar>
                          </v-col>
                          <v-col cols="10" md="10" sm="7">
                            <p
                              style="margin:7px;font-size:20px;padding-left:30px"
                              class="font-weight-bold"
                            >
                              {{ person.name.first }} {{ person.name.last }}
                            </p>
                            <p
                              style="padding-left:40px;font-size:15px"
                              class="font-weight-bold font-italic"
                            >
                              {{ person.location.street.number }},
                              {{ person.location.city }},
                              {{ person.location.state }}
                            </p>
                            <div style="padding-left:22px;margin-top:-30px">
                              <v-row>
                                <v-col cols="12" md="6" sm="5">
                                  <v-btn
                                    color="#f7d9f2"
                                    depressed
                                    text
                                    style="margin-top:23px;border-radius:40px"
                                    ><v-icon color="#BABDD1"
                                      >mdi-email-outline</v-icon
                                    ><span
                                      style="opacity:0.6;color:#262A41;text-align:center;font-size:12px"
                                    >
                                      {{ person.email }}
                                    </span></v-btn
                                  >
                                </v-col>

                                <v-col cols="12" md="4" sm="5">
                                  <v-btn
                                    color="#f7d9f2"
                                    depressed
                                    text
                                    style="margin-top:23px;border-radius:40px"
                                    ><v-icon color="#BABDD1"
                                      >mdi-phone-in-talk-outline</v-icon
                                    ><span
                                      style="opacity:0.6;color:#262A41;text-align:center;font-size:12px"
                                    >
                                      {{ person.phone }}
                                    </span></v-btn
                                  >
                                </v-col>

                                <v-col cols="12" md="2" sm="2">
                                  <v-btn
                                    width="50px"
                                    height="50px"
                                    @click="goNext(i)"
                                    style="border-radius:14px;margin-top:8px"
                                    class="elevation-24 pa-3"
                                    color="#75d6d1"
                                  >
                                    <v-icon class="white--text" medium>
                                      mdi-arrow-right
                                    </v-icon></v-btn
                                  >
                                </v-col>
                              </v-row>
                            </div>
                          </v-col>
                        </v-row>
                      </v-card>
                    </div>
                  </div>

                  <v-row>
                    <v-col>
                      <div style="margin-left:30px">
                        <v-btn
                          rounded
                          height="50px"
                          color="#7946c1"
                          class="white--text"
                        >
                          <v-icon class="px-2"
                            >mdi-cloud-download-outline</v-icon
                          >Download Results</v-btn
                        >
                      </div>
                    </v-col>

                    <v-col>
                      <div style="margin-left:170px;margin-top:10px">
                        <v-btn
                          color="#e2e3ec"
                          small
                          height="40px"
                          width="25px"
                          style="border-radius:10px"
                          ><v-icon color="#262a41"
                            >mdi-chevron-left</v-icon
                          ></v-btn
                        ><v-btn
                          class="mx-2"
                          color="#262a41"
                          style="border-radius:10px"
                          small
                          height="40px"
                          width="25px"
                          ><v-icon class="white--text"
                            >mdi-chevron-right</v-icon
                          ></v-btn
                        >
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>

                <v-window-item :value="2">
                  <div style="padding-top:50px;margin:50px;text-align:left">
                    <h3
                      class="font-weight-bold"
                      style="color:#30344a;font-size:22px"
                    >
                      User List
                    </h3>
                    <p style="font-size:12px">Filter by</p>

                    <v-row justify-start>
                      <v-col cols="8" sm="8" md="8" lg="5">
                        <v-text-field
                          v-model="search"
                          rounded
                          color="#e2e3ec"
                          label="Find in list"
                          filled
                          prepend-inner-icon="mdi-magnify"
                        />
                      </v-col>
                      <v-col order="1" cols="6" sm="4" md="4">
                        <v-select
                          :items="items"
                          label="Country"
                          dense
                          filled
                          rounded
                        ></v-select>
                      </v-col>
                      <v-col order="2" cols="4" sm="3" md="3">
                        <v-switch
                          v-model="switch1"
                          color="#30bbb5"
                          label="Show Country"
                          style="padding-right:20px;font-size:12px;margin-top:-2px"
                          class="mx-3"
                        ></v-switch>
                      </v-col>
                    </v-row>

                    <v-btn text @click="goBack">
                      <v-icon color="#75d6d1" style="margin-right:10px"
                        >mdi-arrow-left</v-icon
                      >RESULTS</v-btn
                    >

                    <div v-for="(person, i) in onePerson" :key="i">
                      <v-row no-gutters>
                        <v-col cols="6" md="3" sm="6">
                          <v-avatar size="200px" class="my-3">
                            <v-img
                              :src="person.picture.large"
                              style="border-radius:200px;border:solid;border-color:#75d6d1;border-width:6px"
                            />
                          </v-avatar>
                        </v-col>
                        <v-col cols="9" md="9" sm="6">
                          <p
                            style="margin-top:20px;font-size:23px;padding-left:80px;color:#30344a"
                            class="font-weight-black"
                          >
                            {{ person.name.title }} {{ person.name.first }}
                            {{ person.name.last
                            }}<span class="font-weight-light ml-2">{{
                              person.dob.age
                            }}</span>
                          </p>
                          <p
                            style="padding-left:80px;font-size:15px;margin-top:-7px"
                          >
                            {{ person.location.street.number }},
                            {{ person.location.city }},
                            {{ person.location.state }}
                          </p>

                          <div style="padding-left:80px">
                            <v-btn rounded color="#e2e3ec" disabled
                              ><v-icon>mdi-email-outline</v-icon
                              ><span style="color:#262A41;padding-left:3px"
                                >{{ person.email }}
                              </span></v-btn
                            >
                            <v-btn
                              color="#f7d9f2"
                              depressed
                              style="margin-top:23px;border-radius:40px;text-align:center"
                              ><span
                                style="opacity:1;color:#262A41;text-align:center;font-size:12px"
                                >JOINED: {{ person.registered.date }}
                              </span></v-btn
                            >
                            <v-btn
                              color="#f7d9f2"
                              depressed
                              text
                              style="margin-left:-8px;margin-top:23px;border-radius:40px;text-align:center"
                              ><v-icon color="#BABDD1"
                                >mdi-phone-in-talk-outline</v-icon
                              ><span
                                style="opacity:1;color:#BABDD1;text-align:center;font-size:12px"
                              >
                                {{ person.phone }}
                              </span></v-btn
                            >
                            <div style="margin-top:-20px">
                              <v-btn
                                color="#f7d9f2"
                                depressed
                                text
                                style="margin-left:-8px;margin-top:23px;border-radius:40px;text-align:center"
                                ><v-icon color="#BABDD1"
                                  >mdi-cellphone-iphone</v-icon
                                ><span
                                  style="opacity:1;color:#BABDD1;text-align:center;font-size:12px"
                                >
                                  {{ person.cell }}
                                </span></v-btn
                              >
                            </div>
                          </div>
                        </v-col>
                      </v-row>
                    </div>
                  </div>

                  <v-row>
                    <v-col>
                      <div style="margin-left:30px">
                        <v-btn
                          rounded
                          height="50px"
                          color="#7946c1"
                          class="white--text"
                          style="opacity:0.3"
                        >
                          <v-icon class="px-2"
                            >mdi-cloud-download-outline</v-icon
                          >Download Results</v-btn
                        >
                      </div>
                    </v-col>

                    <v-col>
                      <div style="margin-left:170px;margin-top:10px">
                        <v-btn
                          color="#e2e3ec"
                          small
                          height="40px"
                          width="25px"
                          style="border-radius:10px;opacity:0.3"
                          ><v-icon color="#262a41"
                            >mdi-chevron-left</v-icon
                          ></v-btn
                        ><v-btn
                          class="mx-2"
                          color="#262a41"
                          style="border-radius:10px;opacity:0.3"
                          small
                          height="40px"
                          width="25px"
                          ><v-icon class="white--text"
                            >mdi-chevron-right</v-icon
                          ></v-btn
                        >
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
              </v-window>
            </v-card>
          </div>
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",

  data: () => ({
    switch1: true,
    search: "",
    step: 1,
    post: 3,
    api: `https://randomuser.me/api/?results=3`,
    people: [],
    onePerson: [],
    alignments: ["start", "center", "end"],
    items: [
      "Afghanistan",
      "Albania",
      "Algeria",
      "American Samoa",
      "Andorra",
      "Angola",
      "Anguilla",
      "Antarctica",
      "Antigua and Barbuda",
      "Argentina",
      "Armenia",
      "Aruba",
      "Australia",
      "Austria",
      "Azerbaijan",
      "Bahamas (the)",
      "Bahrain",
      "Bangladesh",
      "Barbados",
      "Belarus",
      "Belgium",
      "Belize",
      "Benin",
      "Bermuda",
      "Bhutan",
      "Bolivia (Plurinational State of)",
      "Bonaire, Sint Eustatius and Saba",
      "Bosnia and Herzegovina",
      "Botswana",
      "Bouvet Island",
      "Brazil",
      "British Indian Ocean Territory (the)",
      "Brunei Darussalam",
      "Bulgaria",
      "Burkina Faso",
      "Burundi",
      "Cabo Verde",
      "Cambodia",
      "Cameroon",
      "Canada",
      "Cayman Islands (the)",
      "Central African Republic (the)",
      "Chad",
      "Chile",
      "China",
      "Christmas Island",
      "Cocos (Keeling) Islands (the)",
      "Colombia",
      "Comoros (the)",
      "Congo (the Democratic Republic of the)",
      "Congo (the)",
      "Cook Islands (the)",
      "Costa Rica",
      "Croatia",
      "Cuba",
      "Curaçao",
      "Cyprus",
      "Czechia",
      "Côte d'Ivoire",
      "Denmark",
      "Djibouti",
      "Dominica",
      "Dominican Republic (the)",
      "Ecuador",
      "Egypt",
      "El Salvador",
      "Equatorial Guinea",
      "Eritrea",
      "Estonia",
      "Eswatini",
      "Ethiopia",
      "Falkland Islands (the) [Malvinas]",
      "Faroe Islands (the)",
      "Fiji",
      "Finland",
      "France",
      "French Guiana",
      "French Polynesia",
      "French Southern Territories (the)",
      "Gabon",
      "Gambia (the)",
      "Georgia",
      "Germany",
      "Ghana",
      "Gibraltar",
      "Greece",
      "Greenland",
      "Grenada",
      "Guadeloupe",
      "Guam",
      "Guatemala",
      "Guernsey",
      "Guinea",
      "Guinea-Bissau",
      "Guyana",
      "Haiti",
      "Heard Island and McDonald Islands",
      "Holy See (the)",
      "Honduras",
      "Hong Kong",
      "Hungary",
      "Iceland",
      "India",
      "Indonesia",
      "Iran (Islamic Republic of)",
      "Iraq",
      "Ireland",
      "Isle of Man",
      "Israel",
      "Italy",
      "Jamaica",
      "Japan",
      "Jersey",
      "Jordan",
      "Kazakhstan",
      "Kenya",
      "Kiribati",
      "Korea (the Democratic People's Republic of)",
      "Korea (the Republic of)",
      "Kuwait",
      "Kyrgyzstan",
      "Lao People's Democratic Republic (the)",
      "Latvia",
      "Lebanon",
      "Lesotho",
      "Liberia",
      "Libya",
      "Liechtenstein",
      "Lithuania",
      "Luxembourg",
      "Macao",
      "Madagascar",
      "Malawi",
      "Malaysia",
      "Maldives",
      "Mali",
      "Malta",
      "Marshall Islands (the)",
      "Martinique",
      "Mauritania",
      "Mauritius",
      "Mayotte",
      "Mexico",
      "Micronesia (Federated States of)",
      "Moldova (the Republic of)",
      "Monaco",
      "Mongolia",
      "Montenegro",
      "Montserrat",
      "Morocco",
      "Mozambique",
      "Myanmar",
      "Namibia",
      "Nauru",
      "Nepal",
      "Netherlands (the)",
      "New Caledonia",
      "New Zealand",
      "Nicaragua",
      "Niger (the)",
      "Nigeria",
      "Niue",
      "Norfolk Island",
      "Northern Mariana Islands (the)",
      "Norway",
      "Oman",
      "Pakistan",
      "Palau",
      "Palestine, State of",
      "Panama",
      "Papua New Guinea",
      "Paraguay",
      "Peru",
      "Philippines (the)",
      "Pitcairn",
      "Poland",
      "Portugal",
      "Puerto Rico",
      "Qatar",
      "Republic of North Macedonia",
      "Romania",
      "Russian Federation (the)",
      "Rwanda",
      "Réunion",
      "Saint Barthélemy",
      "Saint Helena, Ascension and Tristan da Cunha",
      "Saint Kitts and Nevis",
      "Saint Lucia",
      "Saint Martin (French part)",
      "Saint Pierre and Miquelon",
      "Saint Vincent and the Grenadines",
      "Samoa",
      "San Marino",
      "Sao Tome and Principe",
      "Saudi Arabia",
      "Senegal",
      "Serbia",
      "Seychelles",
      "Sierra Leone",
      "Singapore",
      "Sint Maarten (Dutch part)",
      "Slovakia",
      "Slovenia",
      "Solomon Islands",
      "Somalia",
      "South Africa",
      "South Georgia and the South Sandwich Islands",
      "South Sudan",
      "Spain",
      "Sri Lanka",
      "Sudan (the)",
      "Suriname",
      "Svalbard and Jan Mayen",
      "Sweden",
      "Switzerland",
      "Syrian Arab Republic",
      "Taiwan",
      "Tajikistan",
      "Tanzania, United Republic of",
      "Thailand",
      "Timor-Leste",
      "Togo",
      "Tokelau",
      "Tonga",
      "Trinidad and Tobago",
      "Tunisia",
      "Turkey",
      "Turkmenistan",
      "Turks and Caicos Islands (the)",
      "Tuvalu",
      "Uganda",
      "Ukraine",
      "United Arab Emirates (the)",
      "United Kingdom of Great Britain and Northern Ireland (the)",
      "United States Minor Outlying Islands (the)",
      "United States of America (the)",
      "Uruguay",
      "Uzbekistan",
      "Vanuatu",
      "Venezuela (Bolivarian Republic of)",
      "Viet Nam",
      "Virgin Islands (British)",
      "Virgin Islands (U.S.)",
      "Wallis and Futuna",
      "Western Sahara",
      "Yemen",
      "Zambia",
      "Zimbabwe",
      "Åland Islands",
    ],
  }),

  created() {
    axios.get(this.api).then((response) => {
      this.people = response.data.results;
      console.log(this.people.slice(0, 1));
      console.log(this.people[1]);
    });
  },

  methods: {
    refresh() {
      location.reload();
    },
    forMale() {
      this.api = "https://randomuser.me/api/?gender=male&results=3";
      axios.get(this.api).then((response) => {
        this.people = response.data.results;
      });
    },

    forFemale() {
      this.api = "https://randomuser.me/api/?gender=female&results=3";
      axios.get(this.api).then((response) => {
        this.people = response.data.results;
      });
    },
    goNext(i) {
      this.step = 2;
      console.log(i);
      this.onePerson = this.people.slice(i, i + 1);
    },

    goBack() {
      this.step = 1;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,400;0,700;1,100&display=swap");

html,
body {
  font-family: "Poppins", sans-serif;
}

#app {
  font-family: "Poppins", sans-serif;
}

.v-btn {
  text-transform: none !important;
}
</style>
