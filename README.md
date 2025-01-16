# Add-two-numbe
import json

def lambda_handler(event, context):
    # Extract numbers from the request payload
    try:
        number1 = event['number1']
        number2 = event['number2']

        # Ensure the inputs are numeric
        if not isinstance(number1, (int, float)) or not isinstance(number2, (int, float)):
            raise ValueError("Inputs must be numeric.")

        # Calculate the sum
        result = number1 + number2

        # Return the result
        return {
            'statusCode': 200,
            'body': json.dumps({
                'result': result
            })
        }

    except KeyError as e:
        return {
            'statusCode': 400,
            'body': json.dumps({
                'error': f"Missing key: {str(e)}. Expected 'number1' and 'number2'."
            })
        }
    except ValueError as e:
        return {
            'statusCode': 400,
            'body': json.dumps({
                'error': str(e)
            })
        }
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps({
                'error': "An error occurred.",
                'details': str(e)
            })
        }
