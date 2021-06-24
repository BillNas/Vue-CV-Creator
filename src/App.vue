<template>
  <div class="container">
    <h1 class="display-2">
      <div class="thumb">VUE JS</div> CV CREATOR
    </h1>
    <hr />
    <form
      class="form"
      @submit.prevent="createPDF()"
    >
      <div class="row">
        <div class="col-md-3 col-sm-3">
          <h2 class="display-5">Personal Information</h2>
          <hr />
          <div class="form-group">
            <label>Name</label>
            <input
              type="text"
              class="form-control"
              v-model="personalInfo.name"
            />
          </div>
          <div class="form-group">
            <label>Email</label>
            <input
              type="email"
              class="form-control"
              v-model="personalInfo.email"
            />
          </div>
          <div class="form-group">
            <label>Social Media</label>
            <select
              class="form-control"
              v-model="personalInfo.gender"
            >
              <option
                v-for="social in personalInfo.socialMedia"
                :key="social"
              >{{social}}</option>
            </select>
            <label>Social Media Link</label>
            <input
              type="text"
              class="form-control"
              v-model="personalInfo.socialMediaUrl"
            />
          </div>
          <div class="form-group">
            <label>Few words about you</label>
            <textarea
              class="form-control"
              rows="3"
              v-model="personalInfo.summary"
            ></textarea>
          </div>
          <div class="form-group">
            <label for="exampleFormControlSelect2">Gender</label>
            <select
              class="form-control"
              v-model="personalInfo.gender"
            >
              <option>Male</option>
              <option>Female</option>
              <option>Other</option>
            </select>
          </div>
          <div class="form-group">
            <label>Age</label>
            <input
              type="number"
              class="form-control"
              v-model="personalInfo.age"
            />
          </div>

          <div class="form-group">
            <label>Citizenship</label>
            <input
              type="text"
              class="form-control"
              v-model="personalInfo.citizenship"
            />
          </div>
          <div class="form-group">
            <label>Country</label>
            <input
              type="text"
              class="form-control"
              v-model="personalInfo.country"
            />
          </div>
          <div class="form-group">
            <label>Hometown</label>
            <input
              type="text"
              class="form-control"
              v-model="personalInfo.hometown"
            />
          </div>
          <div class="form-group">
            <label>Address</label>
            <input
              type="text"
              class="form-control"
              v-model="personalInfo.address"
            />
          </div>
          <div class="form-group">
            <label>Date of Birth</label>
            <input
              type="date"
              class="form-control"
              v-model="personalInfo.birthDate"
            />
          </div>
        </div>

        <div class="col-md-3 col-sm-3">
          <h2 class="display-5">Work Experience</h2>
          <hr />
          <div class="form-group">
            <label>Position</label>
            <input
              type="text"
              class="form-control"
              v-model="workExperience.position"
            />
          </div>
          <div class="form-group">
            <label>Employer</label>
            <input
              type="text"
              class="form-control"
              v-model="workExperience.employer"
            />
          </div>
          <div class="form-group">
            <label for="exampleFormControlTextarea1">Few words about your work</label>
            <textarea
              class="form-control"
              rows="3"
              v-model="workExperience.responsibilities"
            ></textarea>
          </div>
          <div class="form-group">
            <label>Country</label>
            <input
              type="text"
              class="form-control"
              v-model="workExperience.country"
            />
          </div>
          <div class="form-group">
            <label>City</label>
            <input
              type="text"
              class="form-control"
              v-model="workExperience.city"
            />
          </div>
          <div class="form-group">
            <label>From</label>
            <input
              type="date"
              class="form-control"
              v-model="workExperience.from"
            />
          </div>
          <div class="form-group">
            <label>Up To</label>
            <input
              type="date"
              class="form-control"
              v-model="workExperience.upTo"
            />
          </div>
          <button
            @click.prevent="saveWorkExperience()"
            class="btn btn-primary btn-lg mt-2"
          >Save</button>
        </div>
        <br />

        <div class="col-md-3 col-sm-3">
          <h2 class="display-5 ">Education Experience</h2>
          <hr />
          <div class="form-group">
            <label>Degree</label>
            <input
              type="text"
              class="form-control"
              v-model="education.degree"
            />
          </div>
          <div class="form-group">
            <label>Provider</label>
            <input
              type="text"
              class="form-control"
              v-model="education.provider"
            />
          </div>
          <div class="form-group">
            <label>Grade</label>
            <input
              type="number"
              class="form-control"
              v-model="education.grade"
            />
          </div>
          <div class="form-group">
            <label>Country</label>
            <input
              type="text"
              class="form-control"
              v-model="education.country"
            />
          </div>
          <div class="form-group">
            <label>City</label>
            <input
              type="text"
              class="form-control"
              v-model="education.city"
            />
          </div>
          <div class="form-group">
            <label>From</label>
            <input
              type="date"
              class="form-control"
              v-model="education.from"
            />
          </div>
          <div class="form-group">
            <label>Up To</label>
            <input
              type="date"
              class="form-control"
              v-model="education.upTo"
            />
          </div>
          <button
            @click.prevent="saveEducation()"
            class="btn btn-primary btn-lg mt-2"
          >Save</button>
        </div>
      </div>
      <button
        type="submit"
        class="btn btn-success mt-2"
      >Create</button>
    </form>
  </div>
</template>

<script>
/* eslint-disable */
import jsPDF from "jspdf";
import "jspdf-autotable";

export default {
  data() {
    return {
      workExperienceSubmitted: [],
      workRow: [],
      educationRow: [],
      personalInfo: {
        name: "",
        summary: null,
        gender: null,
        phone: null,
        address: null,
        birthDate: null,
        citizenship: null,
        email: null,
        country: null,
        hometown: null,
        socialMedia: [
          "Facebook",
          "Twitter",
          "Github",
          "LinkedIn",
          "Instagram",
          "Youtube"
        ],
        socialMediaUrl: ""
      },
      workExperience: {
        position: null,
        employer: null,
        city: null,
        country: null,
        from: null,
        upTo: null,
        responsibilities: null
      },
      education: {
        degree: null,
        provider: null,
        city: null,
        country: null,
        from: null,
        upTo: null,
        grade: null
      }
    };
  },
  methods: {
    showSuccessAlert() {
      this.$fire({
        text: "Saved successfully.",
        type: "success",
        timer: 3000
      }).then(r => {
        console.log(r.value);
      });
    },
    showErrorAlert() {
      this.$fire({
        title: "Error!",
        text: "Please fill out all fields.",
        type: "error",
        timer: 3000
      }).then(r => {
        console.log(r.value);
      });
    },

    async saveWorkExperience() {
      try {
        if (
          this.workExperience.position &&
          this.workExperience.employer &&
          this.workExperience.city &&
          this.workExperience.country &&
          this.workExperience.from &&
          this.workExperience.upTo &&
          this.workExperience.responsibilities
        ) {
          await this.workRow.push([
            [
              "Position: " + this.workExperience.position,
              "Employer: " + this.workExperience.employer,
              "City: " + this.workExperience.city,
              "Country: " + this.workExperience.country,
              "From: " + this.workExperience.from,
              "Up To: " + this.workExperience.upTo,
              "Responsibilitie: " + this.workExperience.responsibilities
            ]
          ]);
          this.showSuccessAlert();
        } else {
          this.showErrorAlert();
        }
      } catch (error) {
        console.log(error);
      }
    },
    async saveEducation() {
      try {
        if (
          this.education.provider &&
          this.education.degree &&
          this.education.grade &&
          this.education.city &&
          this.education.country &&
          this.education.from &&
          this.education.upTo
        ) {
          await this.educationRow.push([
            [
              "Degree: " + this.education.degree,
              "Provider: " + this.education.provider,
              "Grade: " + this.education.grade,
              "City: " + this.education.city,
              "Country: " + this.education.country,
              "From: " + this.education.from,
              "Up To: " + this.education.upTo
            ]
          ]);
          this.showSuccessAlert();
          this.education.provider = this.education.degree = this.education.grade = this.education.city = this.education.country = this.education.from = this.education.upTo =
            "";
        } else {
          this.showErrorAlert();
        }
      } catch (error) {
        console.log(error);
      }
    },

    createPDF() {
      var doc = new jsPDF();
      var col1 = ["Personal Information"];
      var col2 = ["Work Experience"];
      var col3 = ["Education"];

      var personalInfoRow = [
        ["Name: " + this.personalInfo.name],
        ["Summary: " + this.personalInfo.summary],
        ["Email: " + this.personalInfo.email],
        ["Gender: " + this.personalInfo.gender],
        ["Phone: " + this.personalInfo.phone],
        ["Address: " + this.personalInfo.address],
        ["Date Of Birth: " + this.personalInfo.birthDate],
        ["Citizenship: " + this.personalInfo.citizenship],
        ["Country: s" + this.personalInfo.country],
        ["Hometown: " + this.personalInfo.hometown]
      ];

      doc.autoTable(col1, personalInfoRow, { startY: 10 });
      doc.autoTable(col2, this.workRow, { startY: 110 });
      doc.autoTable(col3, this.educationRow, { startY: 150 });
      doc.save(`${this.personalInfo.name}-CV.pdf`);
    }
  }
};
</script>

<style lang="scss">
.thumb {
  color: rgb(2, 230, 150);
}
form {
  font-size: 20px;
}
</style>
