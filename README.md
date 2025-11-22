import React from "react";
import {
  View,
  Text,
  StyleSheet,
  SafeAreaView,
  TouchableOpacity,
  Switch,
  ScrollView,
} from "react-native";
import Icon from "react-native-vector-icons/MaterialIcons"; // Assuming you use react-native-vector-icons

// --- Component Definition ---

const MedicalIdScreen = () => {
  const [isNotesVisible, setIsNotesVisible] = React.useState(true);

  // Placeholder Data
  const medicalData = {
    name: "CASTRO N KABURU",
    dob: "04/01/2004 (21)",
    bloodType: "O+",
    conditions: ["Diabetes (Type 1)", "Asthma"],
    allergies: ["Penicillin", "Peanuts"],
    medications: [
      "Insulin (Fast-Acting), 10 units before meals, 3xx dx daily, for T1D",
    ],
    organDonor: "YES",
    specialInstructions: "Prone to seizures.",
    contact1: "Tim M (Friend)",
    contact2: "Ronny K (Friend)",
  };

  // Helper component for section titles
  const SectionTitle = ({ title }) => (
    <Text style={styles.sectionTitle}>{title}</Text>
  );

  // Helper component for emergency contacts with a CALL button
  const ContactRow = ({ name, number }) => (
    <View style={styles.contactRow}>
      <Text style={styles.dataText}>{name}</Text>
      <TouchableOpacity
        style={styles.callButton}
        onPress={() => {
          /* Call function */
        }}
      >
        <Text style={styles.callButtonText}>CALL</Text>
      </TouchableOpacity>
    </View>
  );

  return (
    <SafeAreaView style={styles.container}>
      <ScrollView contentContainerStyle={styles.scrollContent}>
        {/* EMERGENCY PROFILE HEADER */}
        <View style={styles.header}>
          <Icon
            name="local-hospital"
            size={20}
            color="#FFFFFF"
            style={{ marginRight: 8 }}
          />
          <Text style={styles.headerText}>EMERGENCY PROFILE</Text>
        </View>

        {/* PROFILE DATA */}
        <Text style={styles.nameText}>{medicalData.name}</Text>

        <ContactRow name={medicalData.contact1} number="0745799633" />
        <ContactRow name={medicalData.contact2} number="0791182653" />

        <View style={styles.divider} />

        <Text style={styles.dataText}>**DOB / AGE:** {medicalData.dob}</Text>
        <Text style={styles.dataText}>
          **BLOOD TYPE:** {medicalData.bloodType}
        </Text>

        <View style={styles.divider} />

        {/* MEDICAL CONDITIONS & ALLERGIES */}
        <SectionTitle title="MEDICAL CONDITIONS & ALLERGIES" />
        <Text style={styles.dataText}>**CHRONIC CONDITIONS:**</Text>
        {medicalData.conditions.map((item, index) => (
          <Text key={`cond-${index}`} style={styles.listItem}>
            * {item}
          </Text>
        ))}
        <Text style={styles.dataText}>**ALLERGIES:**</Text>
        {medicalData.allergies.map((item, index) => (
          <Text key={`allergy-${index}`} style={styles.listItem}>
            * {item}
          </Text>
        ))}

        <View style={styles.divider} />

        {/* MEDICATIONS */}
        <SectionTitle title="MEDICATIONS" />
        {medicalData.medications.map((item, index) => (
          <Text key={`med-${index}`} style={styles.dataText}>
            {item}
          </Text>
        ))}

        <View style={styles.divider} />

        {/* OTHER IMPORTANT NOTES */}
        <SectionTitle title="OTHER IMPORTANT NOTES" />
        <View style={styles.noteRow}>
          <View>
            <Text style={styles.dataText}>
              **ORGAN DONOR:** {medicalData.organDonor}
            </Text>
            <Text style={styles.listItem}>
              * {medicalData.specialInstructions}
            </Text>
          </View>
          {/* Example of a user-facing toggle */}
          <Switch
            value={isNotesVisible}
            onValueChange={setIsNotesVisible}
            trackColor={{ false: "#767577", true: "#81b0ff" }}
            thumbColor={isNotesVisible ? "#f5dd4b" : "#f4f3f4"}
          />
        </View>

        {/* EDIT BUTTON */}
        <TouchableOpacity
          style={styles.editButton}
          onPress={() => {
            /* Navigate to Edit Screen */
          }}
        >
          <Text style={styles.editButtonText}>EDIT MY INFORMATION</Text>
        </TouchableOpacity>

        <Text style={styles.footerText}>Data last updated. Nov 18, 2025</Text>
      </ScrollView>
    </SafeAreaView>
  );
};

// --- Styling ---

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#1C1C1E", // Dark background for contrast
  },
  scrollContent: {
    padding: 20,
  },
  header: {
    flexDirection: "row",
    alignItems: "center",
    backgroundColor: "#FF3B30", // Red for emergency visibility
    padding: 10,
    borderRadius: 8,
    marginBottom: 20,
  },
  headerText: {
    color: "#FFFFFF",
    fontSize: 16,
    fontWeight: "bold",
  },
  nameText: {
    color: "#FFFFFF",
    fontSize: 28,
    fontWeight: "bold",
    marginBottom: 20,
  },
  contactRow: {
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    paddingVertical: 8,
  },
  callButton: {
    backgroundColor: "#34C759", // Green call button
    paddingHorizontal: 15,
    paddingVertical: 5,
    borderRadius: 15,
  },
  callButtonText: {
    color: "#FFFFFF",
    fontWeight: "bold",
    fontSize: 12,
  },
  divider: {
    height: 1,
    backgroundColor: "#3A3A3C", // Lighter grey line
    marginVertical: 15,
  },
  sectionTitle: {
    color: "#AAAAAA", // Light grey for section headers
    fontSize: 14,
    fontWeight: "bold",
    marginTop: 10,
    marginBottom: 5,
  },
  dataText: {
    color: "#FFFFFF",
    fontSize: 16,
    marginBottom: 5,
  },
  listItem: {
    color: "#FFFFFF",
    fontSize: 16,
    marginLeft: 10,
    marginBottom: 5,
  },
  noteRow: {
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginTop: 10,
    marginBottom: 20,
  },
  editButton: {
    backgroundColor: "#007AFF", // Standard iOS/App blue
    padding: 15,
    borderRadius: 10,
    alignItems: "center",
    marginTop: 30,
    marginBottom: 10,
  },
  editButtonText: {
    color: "#FFFFFF",
    fontSize: 18,
    fontWeight: "bold",
  },
  footerText: {
    color: "#AAAAAA",
    fontSize: 12,
    textAlign: "center",
    marginTop: 10,
  },
});

export default MedicalIdScreen;
