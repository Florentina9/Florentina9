import io.restassured.http.ContentType;
import org.apache.http.HttpStatus;
import org.junit.jupiter.api.Test;

import static io.restassured.RestAssured.given;

public class HomeworkPET {

    @Test
    public void addPetTest() {
         given().baseUri("http://api.petclinic.mywire.org")
                .basePath("/petclinic")
                .port(80)
                .contentType(ContentType.JSON)
                .body("\n" +
                        "{\n" +
                        "  \"birthDate\": \"2010/05/23\",\n" +
                        "  \"id\": null,\n" +
                        "  \"name\": \"Lucy\",\n" +
                        "  \"owner\": {\n" +
                        "    \"address\": \"Dristor\",\n" +
                        "    \"city\": \"Bucuresti\",\n" +
                        "    \"firstName\": \"Florentina\",\n" +
                        "    \"id\": 2,\n" +
                        "    \"lastName\": \"Dunica\",\n" +
                        " \"pets\": [\n" + null +
                        " \"telephone\": \"0753980245\"},\n" +
                        " \"type\": {\n" +
                        " \"id\": 2,\n" +
                        " \"name\": \"Lucy\"},\n" +
                        " \"visits\": [\n" +
                        " {\n" +
                        " \"date\": \"2020/06/08\",\n" +
                        " \"description\": \"Happy\",\n" +
                        " \"id\": null\n" +
                        "}\n" +
                        "]\n" +
                        "}")

                .when().log().all()
                .post("/api/pets/").prettyPeek()
                .then()
                .statusCode(HttpStatus.SC_CREATED);
    }

    //get pet list
    @Test
    public void getPet() {
        given().baseUri("http://api.petclinic.mywire.org")
                .basePath("/petclinic")
                .port(80)
                .when()
                .get("/api/pets")
                .prettyPeek()
                .then()
                .statusCode(HttpStatus.SC_OK);

    }
}
