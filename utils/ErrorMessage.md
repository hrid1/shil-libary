ErrorMessage Component
A reusable React component for displaying form validation errors, designed for use with react-hook-form.
Installation
Ensure react-hook-form is installed:
npm install react-hook-form

Component Code
Save this in ErrorMessage.tsx:
import { FieldError } from "react-hook-form";

interface ErrorMessageProps {
  error?: FieldError;
  defaultMessage?: string;
}

export const ErrorMessage: React.FC<ErrorMessageProps> = ({
  error,
  defaultMessage = "This field is required",
}) => {
  if (!error) return null;

  return (
    <p className="text-xs text-red-500 mt-1">
      {error.message || defaultMessage}
    </p>
  );
};

Usage Example
Below is a minimalist example of using the ErrorMessage component in a form with react-hook-form.
import { useForm } from "react-hook-form";
import { ErrorMessage } from "./ErrorMessage";

interface FormInputs {
  username: string;
}

export const MyForm: React.FC = () => {
  const { register, handleSubmit, formState: { errors } } = useForm<FormInputs>();

  const onSubmit = (data: FormInputs) => {
    console.log("Form Data:", data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <label htmlFor="username">Username</label>
      <input
        id="username"
        {...register("username", { required: "Username is required" })}
      />
      <ErrorMessage error={errors.username} />
      <button type="submit">Submit</button>
    </form>
  );
};

Props



Prop
Type
Description
Default Value



error
FieldError
The error object from react-hook-form.
undefined


defaultMessage
string
Fallback message if error.message is missing.
"This field is required"


Notes

Use with react-hook-form for type-safe error handling.
Customize styling by modifying the className in the <p> element.
Ensure Tailwind CSS (or equivalent) is set up for the default styling (text-xs text-red-500 mt-1).
